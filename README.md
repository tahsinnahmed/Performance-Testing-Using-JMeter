<img width="1919" height="987" alt="LOG 4" src="https://github.com/user-attachments/assets/6a0d30b6-73aa-4968-88f9-fbd14107a748" /># Performance Testing Using JMeter

This project provides a complete **API Performance Test using Apache JMeter** for testing all **Authenticated Endpoints** of:

👉 Source Link: https://api.restful-api.dev

<img width="1754" height="984" alt="API Source" src="https://github.com/user-attachments/assets/6bc17ab9-163e-41e5-9054-5dab67035b32" />

It covers:

* ✅ Register
* ✅ Login
* ✅ GET (Collections & Objects)
* ✅ POST (Create Object)
* ✅ PUT (Full Update)
* ✅ PATCH (Partial Update)
* ✅ DELETE (Remove Object)

---

# Project Structure

```
Performance Testing Using JMeter/
│── Test Result/
│   └── AUTH (Login)/
│       └── LOG 1.png
│       └── LOG 2.png
│       └── LOG 3.png
│       └── LOG 4.png
│   └── AUTH (Register)/
│       └── REG 1.png
│       └── REG 2.png
│       └── REG 3.png
│       └── REG 4.png
│   └── DELETE/
│       └── DEL 1.png
│       └── DEL 2.png
│       └── DEL 3.png
│       └── DEL 4.png
│   └── GET/
│       └── GET 1.png
│       └── GET 2.png
│       └── GET 3.png
│       └── GET 4.png
│   └── PATCH/
│       └── PAT 1.png
│       └── PAT 2.png
│       └── PAT 3.png
│       └── PAT 4.png
│   └── POST/
│       └── POS 1.png
│       └── POS 2.png
│       └── POS 3.png
│       └── POS 4.png
│   └── PUT/
│       └── PUT 1.png
│       └── PUT 2.png
│       └── PUT 3.png
│       └── PUT 4.png
│    ── API Source.png
│    ── HTTP Header Manager.png
│    ── View Result in Table.png
│── API Testing.jmx
│── logs.txt
│── README.md
```

---

# Prerequisites

* Install Apache JMeter
* API Key from https://restful-api.dev

---

# Global Configuration in JMeter

## 1. Test Plan Setup

* Thread Group:

  * Threads: 1
  * Ramp-up: 1
  * Loop Count: 1

---

## 2. HTTP Request Defaults

| Field       | Value               |
| ----------- | ------------------- |
| Protocol    | https               |
| Server Name | api.restful-api.dev |

---

## 3. HTTP Header Manager

Add:

```
x-api-key: YOUR_API_KEY
Content-Type: application/json
```

<img width="1910" height="679" alt="HTTP Header Manaager" src="https://github.com/user-attachments/assets/78841b6e-68da-4b21-9834-ee7489bd6490" />

---

# 1. Register Request

## Sampler

```
POST /register?auth-type=jwt
```

## Body

```json
{
  "email": "ahmed@test.com",
  "password": "SecurePassword123",
  "name": "Tahsin Ahmed"
}
```

<img width="1918" height="729" alt="REG 1" src="https://github.com/user-attachments/assets/6ac3f4b7-90ec-426d-8f80-e8dc8ee13527" />

## Post-Processor (JSON Extractor)

Extract:

* `token` → `${jwt_token}`
---

<img width="1914" height="672" alt="REG 3" src="https://github.com/user-attachments/assets/ac3eb6a9-2916-49cb-9f6a-1b5d178f99ca" />
<img width="1915" height="996" alt="REG 4" src="https://github.com/user-attachments/assets/85a71485-853b-45b6-9464-fbd5b97a9bb4" />

# 2. Login Request

## Sampler

```
POST /login?auth-type=jwt
```

## Body

```json
{
  "email": "antonio@example.com",
  "password": "SecurePassword123"
}
```

## JSON Extractor

* `token` → `${jwt_token}`
---

<img width="1912" height="1008" alt="LOG 2" src="https://github.com/user-attachments/assets/b3770569-3373-4e67-be72-eabf2680388b" />

# Add Authorization Header (After Login)

Add another **HTTP Header Manager**:

```
Authorization: Bearer ${jwt_token}
```

<img width="1919" height="987" alt="LOG 4" src="https://github.com/user-attachments/assets/364eaec1-cf9b-43bf-a7b2-78685496f02f" />

---

# 3. GET – All Collections

## Sampler

```
GET /collections/products/objects
```

<img width="1913" height="711" alt="GET 3" src="https://github.com/user-attachments/assets/bfee7289-ebbd-4410-a291-27163529bf99" />
<img width="1915" height="981" alt="GET 4" src="https://github.com/user-attachments/assets/76f59e6b-6b5d-42de-b52c-94e08a0dbc12" />

---

# 4. POST – Create Object

## Sampler

```
POST /collections/products/objects
```

## Body

```json
{
  "name": "Apple MacBook Pro 16",
  "data": {
    "year": 2019,
    "price": 1849.99,
    "CPU model": "Intel Core i9",
    "Hard disk size": "1 TB"
  }
}
```

<img width="1918" height="1026" alt="POS 1" src="https://github.com/user-attachments/assets/2cc5f974-8e66-4723-867a-ac5122a72e57" />

## JSON Extractor

* Extract `id` → `${object_id}`
---

<img width="1913" height="1018" alt="POS 2" src="https://github.com/user-attachments/assets/4afb4ab2-063f-45f5-bacc-fb7afbf166d5" />
<img width="1916" height="1003" alt="POS 4" src="https://github.com/user-attachments/assets/e7a8906a-6870-4cf8-ab72-f942eebd6f4c" />

# 5. PUT – Full Update

## Sampler

```
PUT /collections/products/objects/${object_id}
```

<img width="1915" height="1030" alt="PUT 1" src="https://github.com/user-attachments/assets/40e07b66-8328-45e3-a0f1-a7fba30b7adb" />

## Body

```json
{
  "name": "Apple MacBook Pro 16",
  "data": {
    "year": 2019,
    "price": 2049.99,
    "CPU model": "Intel Core i9",
    "Hard disk size": "1 TB",
    "color": "silver"
  }
}
```

<img width="1915" height="1014" alt="PUT 2" src="https://github.com/user-attachments/assets/a9c50e2d-e1c5-4e23-9151-6ef1858c9e00" />
<img width="1913" height="979" alt="PUT 4" src="https://github.com/user-attachments/assets/550b0b72-13b7-467a-a200-8207d7cfe321" />

---

# 6. PATCH – Partial Update

## Sampler

```
PATCH /collections/products/objects/${object_id}
```

<img width="1914" height="638" alt="PAT 1" src="https://github.com/user-attachments/assets/d73a43ee-1dec-4e04-9436-3771d2f284c7" />

## Body

```json
{
  "name": "Apple MacBook Pro 16 (Updated Name)"
}
```

<img width="1917" height="1024" alt="PAT 2" src="https://github.com/user-attachments/assets/a5fb5849-0205-4052-9c51-5d5ce066d9f5" />
<img width="1915" height="998" alt="PAT 4" src="https://github.com/user-attachments/assets/caa1a67b-2a4b-4315-91a8-6f620f0c348d" />

---

# 7. DELETE – Remove Object

## Sampler

```
DELETE /collections/products/objects/${object_id}
```

<img width="1914" height="676" alt="DEL 3" src="https://github.com/user-attachments/assets/05ea2d0f-c381-4fc5-bfb7-3373442a48be" />
<img width="1915" height="975" alt="DEL 4" src="https://github.com/user-attachments/assets/001beca5-9667-41e8-9e7f-b5dd096ddc47" />

---

# Listeners to Add

* View Results Table
* View Result Tree
  
<img width="1916" height="1030" alt="View Results in Table" src="https://github.com/user-attachments/assets/92677282-590a-44a9-a0a4-1bd2029028a3" />

---

# Assertions (Recommended)

Add **Response Assertion**:

* Status Code = 200 / 201 / 409
* JSON contains expected fields

---

# Tips

* Use **Debug Sampler** to inspect variables
* Use **View Results Tree** for debugging
* Keep thread count low for free API

---

# How to Run

1. Open JMeter
2. Load `API Testing.jmx`
3. Update API Key
4. Click ▶️ Run

---

# License

Free for educational and testing purposes.

---

# Bonus

You can extend this test plan with:

* Load Testing
* Stress Testing
* CI/CD integration (GitHub Actions)

---
