RateLimit.js
============
[![Build
Status](https://travis-ci.org/dudleycarr/ratelimit.js.svg)](https://travis-ci.org/dudleycarr/ratelimit.js) [![npm version](https://badge.fury.io/js/ratelimit.js.svg)](http://badge.fury.io/js/ratelimit.js)

A NodeJS library for efficiently rate limiting using sliding windows stored in Redis.

Features
--------
* Uses a sliding window for a rate limit rule
* Multiple rules per instance
* Multiple instances of RateLimit side-by-side for different categories of users.

Background
----------
See this excellent articles on how the sliding window rate limiting with Redis
works:
[Introduction to Rate Limiting with Redis Part 1](http://www.dr-josiah.com/2014/11/introduction-to-rate-limiting-with.html)
[Introduction to Rate Limiting with Redis Part 2](http://www.dr-josiah.com/2014/11/introduction-to-rate-limiting-with_26.html)

Install
-------

```
npm install ratelimit.js
```

Usage
-----

Basic example:

```javascript
var RateLimit = require('ratelimt.js').RateLimit;
var redis = require('redis');

var client = redis.createClient();

var rules = [
  {interval: 1, limit: 5},
  {interval: 3600, limit: 1000}
  ];
var limiter = RateLimit(client, rules);

var showRatedLimited = function(err, isRateLimited) {
  return console.log("Error: " + err);
  console.log("Is rate limited? " + isRateLimited);
};

// Exceed rate limit.
for(var i = 0; i < 10; i++) {
  limiter.incr '127.0.0.1', function() {};
}
ratelimit.incr('127.0.0.1', isRateLimited);
```


Output:
```
Is rate limited? false
Is rate limited? false
Is rate limited? false
Is rate limited? false
Is rate limited? false
Is rate limited? true
Is rate limited? true
Is rate limited? true
Is rate limited? true
Is rate limited? true
```

ChangeLog
---------
* **1.1.0**
  * Add Express middleware
  * Updated README
  * Added copyrights on Lua code
* **1.0.0**
  * Initial RateLimit support

Authors
-------
[Dudley Carr](https://github.com/dudleycarr)
[Josh Gummersall](https://github.com/joshgummersall)