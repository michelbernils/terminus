---
layout: post
title:  "Idempotency"
date:   2025-08-23 20:07:00 -0300
categories: computer theory
---

# Idempotency

## What is idempotency
Idempotency is the property of an operation that produces the same result no matter how many times it’s executed. In other words, whether you perform the operation once or multiple times, the outcome remains consistent.

#### So this week at work, I had an idempotency issue on my code, every time I sent a POST request, the data was being saved to the database. Let’s recap this concept and see how we can avoid issues like this.

#### REST
1. GET: Are idempotent.
1. POST: Aren't idempotent.
1. PATCH: Aren't idempotency. (just changes the variables you send in the request)
1. PUT: Are idempotent. (changes the full payload)
1. DELETE: Are idempotent.

#### Lets make a POST request

POST - /user
Content-Type: application/json

```json
   {
      "firstName": "Michel",
      "secondName": "Krahenbuhl",
      "documentNumber": "123456789"
   }
```

```json
   {
      "id": 123,
      "firstName": "Michel",
      "secondName": "Krahenbuhl",
      "documentNumber": "123456789"
   }
```

If I make this same request as a form of avoiding using the verb PUT for example, it will create the same person twice, with its data updated. (this can be avoided by adding a unique constraint on documentNumber)

```json
   {
      "firstName": "Michel",
      "secondName": "Krahenbuhl",
      "documentNumber": "123456789"
   }
```

```json
   {
      "id": 1234,
      "firstName": "Michel",
      "secondName": "Krahenbuhl",
      "documentNumber": "123456789"
   }
```

#### Now, let’s try using PUT

PUT - /user/{id}
Content-Type: application/json 

```json
   {
      "firstName": "Michel",
      "secondName": "Krahenbuhl",
      "documentNumber": "123456789"
   }
```

```json
   {
      "id": 123,
      "firstName": "Michel",
      "secondName": "Krahenbuhl",
      "documentNumber": "123456789"
   }
```

Lets call PUT a second time.

PUT - /user/{id} 
Content-Type: application/json

```json
   {
      "firstName": "Michel",
      "secondName": "Krahenbuhl",
      "documentNumber": "123456789"
   }
```

```json
   {
      "id": 123,
      "firstName": "Michel",
      "secondName": "Krahenbuhl",
      "documentNumber": "123456789"
   }
```

#### Idempotency key
An idempotency key is a unique identifier (usually a string or UUID) that a client sends along with a request to ensure the server processes it only once, even if the request is retried multiple times.

{firstName}{secondName}{documentNumber}

For example, when creating a user:

POST - /user
Idempotency-Key: MichelKrahenbuhl123456789
Content-Type: application/json

```json
{
   "firstName": "Michel",
   "secondName": "Krahenbuhl",
   "documentNumber": "123456789"
}




