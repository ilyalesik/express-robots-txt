# express-robots-txt [![npm version](https://badge.fury.io/js/express-robots-txt.svg)](https://badge.fury.io/js/express-robots-txt) ![Node.js CI](https://github.com/modosc/express-robots-txt/workflows/Node.js%20CI/badge.svg)

Express middleware for generating a robots.txt or responding with an existing file. Forked from [weo-edu/express-robots](https://github.com/weo-edu/express-robots). 

## Using a file

```javascript
app.use(robots(__dirname + '/robots.txt'));
```

## Using an object

### Basic object

```javascript
app.use(robots({ UserAgent: '*', Disallow: '/' }))
```

#### Will produce:
```
User-agent: *
Disallow: /
```

### Crawl Delay
You can optionally pass a CrawlDelay in just like passing in Disallow

```javascript
app.use(robots({ UserAgent: '*', Disallow: '/', CrawlDelay: '5' }))
```

#### Will produce:
```
User-agent: *
Disallow: /
Crawl-delay: 5
```
### Sitemap
You can optionally pass a Sitemap in just like passing in CrawlDelay:


```javascript
app.use(robots({ UserAgent: '*', Disallow: '/', CrawlDelay: '5', Sitemap: 'https://nowhere.com/sitemap.xml' }))
```

#### Will produce:
```
User-agent: *
Disallow: /
Crawl-delay: 5
Sitemap: https://nowhere.com/sitemap.xml
```

You can also pass in an array of Sitemaps:

```javascript
app.use(robots({ UserAgent: '*', Disallow: '/', CrawlDelay: '5', Sitemap: ['https://nowhere.com/sitemap.xml', 'https://nowhere.com/sitemap2.xml'] }))
```

#### Will produce:
```
User-agent: *
Disallow: /
Crawl-delay: 5
Sitemap: https://nowhere.com/sitemap.xml
Sitemap: https://nowhere.com/sitemap2.xml
```

### Or an array of objects

```javascript
app.use(robots([
  {
    UserAgent: 'Googlebot',
    Disallow: '/no-google'
  },
  {
    UserAgent: 'Bingbot',
    Disallow: '/no-bing'
  }
]));
```

#### Will produce:
```
User-agent: Googlebot
Disallow: /no-google
User-agent: Bingbot
Disallow: /no-bing
```

### Or either property (UserAgent | Disallow) as an array

```javascript
app.use(robots([
  {
    UserAgent: [ 'Googlebot', 'Slurp' ],
    Disallow: [ '/no-google', '/no-yahoo' ]
  },
  {
    UserAgent: '*',
    Disallow: [ '/no-bots', '/still-no-bots' ]
  }
]));
```

#### Will produce:
```
User-agent: Googlebot
User-agent: Slurp
Disallow: /no-google
Disallow: /no-yahoo
User-agent: *
Disallow: /no-bots
Disallow: /still-no-bots
```
