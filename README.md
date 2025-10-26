
# ALX PWA 0x01 — Movie Database API & CineSeek App

## API Overview

The **MoviesDatabase API** provides access to a vast collection of movie data including titles, genres, release years, cast, crew, and related media. Developers can retrieve trending, popular, and upcoming movies, filter them by year or genre, and get detailed metadata such as images, descriptions, and ratings.

The API supports **pagination**, **filtering**, and **sorting** to help build powerful movie discovery experiences.
It is an ideal backend data source for applications like **CineSeek**, which allows users to browse and explore the latest and most popular movies.

---

## API Version

**Version:** `v1`
**Base URL:** `https://moviesdatabase.p.rapidapi.com`

---

## Available Endpoints

| Endpoint                     | Method | Description                                                                                  |
| ---------------------------- | ------ | -------------------------------------------------------------------------------------------- |
| `/titles`                    | `GET`  | Retrieves a list of movie titles with optional filters like year, genre, or sorting options. |
| `/titles/:id`                | `GET`  | Retrieves detailed information for a specific movie by its unique ID.                        |
| `/titles/search/title/:name` | `GET`  | Searches movies by their title or partial title.                                             |
| `/titles/random`             | `GET`  | Returns random movies, useful for recommendations.                                           |
| `/titles/series/:id`         | `GET`  | Fetches all titles related to a particular movie series or franchise.                        |
| `/titles/utils/genres`       | `GET`  | Returns a list of all available genres.                                                      |
| `/titles/utils/languages`    | `GET`  | Provides a list of supported languages for movie titles.                                     |

---

## Request and Response Format

### Example Request

```bash
GET https://moviesdatabase.p.rapidapi.com/titles?year=2023&limit=10&page=1
```

**Headers:**

```json
{
  "x-rapidapi-key": "YOUR_API_KEY_HERE",
  "x-rapidapi-host": "moviesdatabase.p.rapidapi.com"
}
```

### Example Response

```json
{
  "page": 1,
  "next": 2,
  "entries": 10,
  "results": [
    {
      "id": "tt1234567",
      "primaryImage": {
        "url": "https://example.com/poster.jpg"
      },
      "titleText": {
        "text": "Example Movie"
      },
      "releaseYear": {
        "year": 2023
      }
    }
  ]
}
```

Each movie object may contain:

* `id`: Unique movie identifier (IMDb-like format)
* `primaryImage.url`: Movie poster or promotional image
* `titleText.text`: The movie title
* `releaseYear.year`: The year of release

---

## Authentication

The API uses **RapidAPI key-based authentication**.
Include your API key in every request header.

**Header Example:**

```bash
x-rapidapi-key: YOUR_API_KEY
x-rapidapi-host: moviesdatabase.p.rapidapi.com
```

**In Next.js**, store your key securely in an environment variable:

```bash
# .env.local
MOVIE_API_KEY=YOUR_RAPIDAPI_KEY
```

---

## Error Handling

Common API errors include:

| Status Code | Meaning               | Description                                    |
| ----------- | --------------------- | ---------------------------------------------- |
| `400`       | Bad Request           | Invalid query parameters or malformed request. |
| `401`       | Unauthorized          | Missing or invalid API key.                    |
| `404`       | Not Found             | The requested movie or resource was not found. |
| `429`       | Too Many Requests     | You’ve exceeded your API rate limit.           |
| `500`       | Internal Server Error | A problem occurred on the API’s end.           |

**Example Error Response:**

```json
{
  "message": "Invalid or missing API key",
  "status": 401
}
```

To handle errors safely in your code:

```typescript
if (!response.ok) {
  throw new Error("Something went wrong while fetching movies");
}
```

---

## Usage Limits and Best Practices

### Rate Limits

* **Free Tier** (RapidAPI): typically ~500 requests per month (check your RapidAPI dashboard).
* **Pro Tier**: higher limits for production use.

### Best Practices

* Cache results where possible to reduce redundant requests.
* Use pagination to avoid fetching too many results at once.
* Handle rate limit errors (`429`) with exponential backoff or retry logic.
* Do not expose your API key in the frontend — use Next.js API routes as a secure proxy (like `fetch-movies.ts` in your app).
* Prefer server-side calls for sensitive data.

---

## Tech Stack for CineSeek App

* **Next.js (TypeScript)** – Frontend framework
* **Tailwind CSS** – Styling
* **MoviesDatabase API** – Data provider
* **FontAwesome** – Icons
* **Vercel / Localhost** – Hosting environment

---

## Author

**Name:** Mistire
**Program:** ALX Software Engineering
**Project:** ALX Project 0x14 — MovieApp (CineSeek)
**Year:** 2025

---

