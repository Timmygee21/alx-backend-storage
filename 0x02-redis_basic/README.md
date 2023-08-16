# 0x02. Redis basic  

## Redis Usage Examples

This README file provides examples and guidelines on using Redis to perform various operations such as writing strings, reading from Redis and recovering original types, incrementing values, storing lists, retrieving lists, and implementing an expiring web cache and tracker.  

Table of Contents  
1. [Introduction](https://github.com/Flesier/alx-backend-storage/tree/master/0x02-redis_basic#introduction)
2. [Writing Stringa to Redis](https://github.com/Flesier/alx-backend-storage/tree/master/0x02-redis_basic#writing-strings-to-redis)
3. [Reading from Redis and Recovering Original Type](https://github.com/Flesier/alx-backend-storage/tree/master/0x02-redis_basic#reading-from-redis-and-recovering-original-type)
4. [Incrementing Values](https://github.com/Flesier/alx-backend-storage/tree/master/0x02-redis_basic#incrementing-values)
5. [Storing Lists](https://github.com/Flesier/alx-backend-storage/tree/master/0x02-redis_basic#storing-lists)
6. [Retrieving Lists](https://github.com/Flesier/alx-backend-storage/tree/master/0x02-redis_basic#retrieving-lists)
7. [Implementing an Expiring Web Cache and Tracker](https://github.com/Flesier/alx-backend-storage/tree/master/0x02-redis_basic#implementing-an-expiring-web-cache-and-tracker)
8. [Conclusion](https://github.com/Flesier/alx-backend-storage/tree/master/0x02-redis_basic#conclusion)

## Introduction

Redis is an in-memory data store that can be used as a powerful key-value database and caching solution. In this document, we'll cover some common usage scenarios for Redis, providing code examples in Python to demonstrate each operation.

To follow these examples, you should have Redis installed and accessible in your environment. Additionally, you'll need a Redis client for your programming language. We'll use the redis Python library for these examples.  
`pip install redis`

## Writing Strings to Redis  
To store strings in Redis, we can use the SET command. Here's an example in Python:  
```
import redis

# Connect to Redis
redis_client = redis.StrictRedis(host='localhost', port=6379, db=0)

# Set a string value
redis_client.set('username', 'john_doe')
```

## Reading from Redis and Recovering Original Type  
When we retrieve data from Redis, it returns bytes by default. To recover the original data type, we need to handle the conversion ourselves. Here's an example:  
```
# Get a value from Redis and convert it to string
username = redis_client.get('username').decode('utf-8')
print('Username:', username)
```

## Incrementing Values  
Redis provides atomic operations to increment and decrement integer values. This can be useful for implementing counters and statistics. Here's an example:   
```
# Increment a value
redis_client.set('visits', 0)
redis_client.incr('visits')
```

## Storing Lists  
Redis allows us to store lists as values associated with a key. We can perform various operations on these lists, such as adding elements, removing elements, and retrieving elements by index. Here's an example:   

```
## Push elements to a list
redis_client.rpush('tasks', 'task1')
redis_client.rpush('tasks', 'task2')
```

## Retrieving Lists  
We can retrieve the list from Redis and perform operations like fetching specific elements or getting the entire list. Here's an example: 

```
# Get the whole list
tasks = redis_client.lrange('tasks', 0, -1)

# Get the first element
first_task = redis_client.lindex('tasks', 0)
```

## Implementing an Expiring Web Cache and Tracker  
Redis allows us to set an expiration time for keys. This can be handy when implementing caching or tracking mechanisms. Here's an example of implementing an expiring web cache:   
```
# Cache a webpage for 60 seconds
webpage_url = 'https://example.com/page1'
webpage_content = '...'  # Content of the webpage
redis_client.setex(webpage_url, 60, webpage_content)
```

## To track the number of visits to a webpage:  
```
# Track webpage visits for 24 hours
webpage_url = 'https://example.com/page1'
redis_client.incr(webpage_url)
redis_client.expire(webpage_url, 24 * 60 * 60)  # Set expiration to 24 hours
```
