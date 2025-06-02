# RESTful API Design — Library Catalogue (Simplified Version)

## 1. Functional Requirements
- User can view the list of books
- User can view book details
- User can filter books by category or author
- User can create, update, and delete a book
- User can view all authors and categories

## 2. Non-Functional Requirements
- API should respond in JSON format
- API should respond within 1 second for typical requests
- API should be available 99% of the time

---

## 3. Data Model

### Book
- id: Integer
- title: String
- authorId: Integer
- categoryId: Integer
- publishedYear: Integer

### Author
- id: Integer
- name: String

### Category
- id: Integer
- name: String

---

## 4. REST API Endpoints

### Book Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /books | Get all books |
| GET | /books?authorId=1&categoryId=2 | Filter books by author and category |
| GET | /books/{id} | Get a single book |
| POST | /books | Add a new book |
| PUT | /books/{id} | Update a book |
| DELETE | /books/{id} | Delete a book |

### Author Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /authors | Get all authors |
| GET | /authors/{id} | Get author details |

### Category Endpoints
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | /categories | Get all categories |
| GET | /categories/{id} | Get category details |

---

## 5. Example Status Codes
| Code | Meaning |
|------|---------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 404 | Not Found |
| 500 | Server Error |

---

## 6. Pagination
For large lists, support:
```
GET /books?page=2&size=10
```

---

## 7. Authentication
- Use a simple API key in header:
```
Authorization: ApiKey 123456
```

---

## 8. Caching
- GET /books and GET /books/{id} responses should be cached (e.g., 10 minutes)

---

## 9. Richardson Maturity Model
- Level 3:
    - Uses proper HTTP methods (GET, POST, PUT, DELETE)
    - Uses resource URIs
    - JSON responses
    - Uses HATEOAS
  
---

## Example JSON for Book
```json
{
  "id": 1,
  "title": "The Catcher in the Rye",
  "authorId": 3,
  "_links": {
    "self": {"href": "/books/1"},
    "author": {"href": "/authors/3"},
    "category": {"href": "/categories/2"}
  }
}
```
