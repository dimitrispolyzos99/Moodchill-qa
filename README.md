# MoodChill – API Test Suite (Postman)

Automated Postman tests for the **4 REST APIs** used in [MoodChill](https://github.com/dimitrispolyzos99/MoodChill), an iOS app I built. The suite covers **positive and negative** cases: status codes, response structure, and authentication validation.

## APIs under test

| API | Method | Purpose | Auth |
|-----|--------|---------|------|
| Open-Meteo | GET | Current weather by coordinates | None |
| TVmaze | GET | Search TV shows | None |
| iTunes Search | GET | Search songs | None |
| API-Ninjas Quotes | GET | Quotes by category | API key (header) |

## What's tested

**Positive**
- Status code is `200`
- Response has the expected structure — required fields present, results array is non-empty

**Negative**
- Invalid API key is rejected with a **4xx client error** (auth validation)

## QA notes

- Tests assert **structure, not just status** — a `200` with missing or empty data is still a failure.
- **Empty-result handling:** a valid search term with no matches returns `200` + an empty array. This is the "valid input, no results" equivalence class and is a common source of UI bugs (blank screen / crash) if unhandled.
- The **negative auth test** confirms the API rejects bad credentials with a client error rather than failing silently or returning a server error.

## How to run

1. Import `MoodChill-API-Tests.postman_collection.json` into Postman.
2. For the **Quotes** requests, add your own [API-Ninjas](https://api-ninjas.com/) key in the `X-Api-Key` header. The key is **not included** in this repo for security — the placeholder `YOUR_API_KEY_HERE` marks where it goes.
3. Send each request, or use the **Collection Runner** to run the whole suite at once and view the test results.

---

*Part of my QA portfolio. I'm a self-taught iOS developer moving into QA, with a developer-grade testing mindset — I read code at implementation level to write sharper API and structural tests.*
