# Phoenix API
The Phoenix API app is a Phoenix web application that serves as a public API for retrieving information about a collection of books stored in a database.

## Data in database
### Books
Books have the following properties:

- **id** (integer): The unique identifier for the book.

- **title** (string): The title of the book.

### Pages
Books can have many pages. Pages have the following properties:

- **id** (integer): The unique identifier for the page.

- **order_index** (integer): A zero-based index that indicates the position of a page within a book. This value is unique per book.

- **content** (string): The text content of the page. The content does not include any heading, italic, underline, or bold formatting.

- **status** (string): The status of a page of a book. Possible values: "active" or "inactive". Each book can have one active page at most.

## Setting up the database

To create an instance of the application's database with all its tables and seed it with random books and their pages, run the following command:

```
mix ecto.setup
```

This command performs the following actions:

1. **Creates the Database**: Sets up the database instance required for the application.

1. **Creates Tables**: Generates all necessary tables within the database.

1. **Seeds the Database**: Populates the database with 4,000 books that each have 10 pages. All book and page data is randomly generated.

## Endpoints
The Phoenix API app exposes a collection of endpoints that all return JSON.

### GET `/api/books`
An endpoint for retrieving the books from the database, along with their active page. If a book does not have an active page, the first page is retrieved.

By default, returns all books. See the "Query Parameters" section for endpoint options.

#### Return data
Returns a list of JSON objects with the properties `"book"` and `"page"`.

If a book does not have any pages the `"page"` key has the value `null`.

#### Example return data:

```
[
  {
    "book": {
      "id": 8,
      "title": "Blue Sky"
    },
    "page": {
      "id": 14,
      "order_index": 4,
      "content": "She couldn’t shake the feeling that something"...,
      "status": "active"
    }
  },
    {
    "book": {
      "id": 11,
      "title": "The Hungry Kettle"
    },
    "page": {
      "id": 20,
      "order_index": 0,
      "content": "With one last glance at the darkening forest,"...,
      "status": "inactive"
    }
  }
]
```

#### Query parameters
- **name**: Filters books by their title. The filter is case-insensitive and matches partial names. For example, `/api/books?name=blue` returns all books with `"blue"` in their title, regardless of case.

### GET `/api/books/:id`
An endpoint for retrieving a book by its id, along with its active page. If a book does not have an active page, the first page is retrieved.

The endpoint does not accept any query parameters.

#### Return data
Returns a JSON object with the properties `"book"` and `"page"`.

If a book does not have any pages the `"page"` key has the value `null`.

#### Example return data:
```
{
  "book": {
    "id": 8,
    "title": "Blue Sky"
  },
  "page": {
    "id": 14,
    "order_index": 4,
    "content": "She couldn’t shake the feeling that something"...,
    "status": "active"
  }
}
```