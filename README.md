# IUM-TWEB

University project developed during the third year of the degree, for the
courses *Human-Machine Interaction* (IUM) and *Web Technologies* (TWEB),
plus a small Python project from the same period.

The main part is a full-stack application for booking private lessons,
with a web client and a mobile client sharing the same Java backend.

Developed together with **Marco Nonne**.

## Repository structure

```
IUM-TWEB/
├── TWEB/
│   ├── backend/              Java backend (Servlets, DAO pattern, MySQL)
│   │   └── src/main/java/    DAO, Servlet, utils
│   └── frontend/
│       ├── vue-app/          Single-page web client (Vue 3)
│       └── static-pages/     Static HTML/CSS pages + accessibility validation screenshots
├── Flutter/                  Mobile client (hand-written code only, lib/)
├── HCI/                      Personas and prototype presentation
└── Python/                   Word graph explorer (Tkinter + NetworkX)
```

## Lesson booking application

### Features

- Registration and login with session tokens
- Two roles:
  - **Client**: browses courses, picks a teacher, date and time slot, books
    lessons, and has a personal area with upcoming, completed and cancelled
    lessons
  - **Admin**: manages courses, teachers, teachings (which teacher teaches
    which course) and lessons
- Availability computed per teacher and time slot
- The same HTTP API is used by both the web and the mobile client

### Tech stack

- **Backend**: Java, Servlets, Maven, MySQL, Gson, CORS filter
- **Web client**: Vue 3, Vue Router, Bootstrap 5
- **Mobile client**: Flutter / Dart (GetX for routing and state)
- **Static pages**: HTML5, CSS3, validated with the W3C markup/CSS validators
  and an accessibility checker (screenshots in
  `TWEB/frontend/static-pages/pictures/validation`)

## Word graph explorer (`Python/`)

A small desktop tool that, given two Italian words and a maximum number of
steps, looks for a path between them in a graph built on the fly from an
Italian word list (`words.italian.txt`).

Two words are connected if they:

- differ by exactly **one letter** (weight 10),
- differ by **one added or removed letter** (weight 20),
- are **anagrams** of each other (weight 30).

The graph is explored from both words at the same time (bidirectional
search) to keep the number of visited nodes low. The result is drawn with
NetworkX and Matplotlib: the path is highlighted and its neighbours are
shown around it. If a word is left empty, a random one is picked from the
dictionary. Built with Python, Tkinter, NetworkX and Matplotlib.

## Notes

This repository is published to show the code, so it is not meant to be run
out of the box: build files, IDE configuration and platform folders were
left out on purpose. The backend expects a local MySQL database
(`db_progetto`) and a Tomcat server; the web client expects the backend on
`localhost:8080`.

## Known limitations and possible improvements

It is a university project, and I am aware of some weak points:

- SQL queries are built by string concatenation; prepared statements would
  prevent SQL injection.
- Credentials are sent in the query string on login and registration; they
  should travel in the request body, over HTTPS.
- Parameters are not URL-encoded on the client side.
- Database credentials and server addresses are hard-coded and should come
  from a configuration file or environment variables.

## Authors

- Federico Pitaccolo
- Marco Nonne