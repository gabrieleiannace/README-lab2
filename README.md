# BigLab 2 - Class: 2022 AW1

## Team name: TEAM_NAME

Team members:
* s305383 Iannace Gabriele
* s123456 LASTNAME FIRSTNAME 
* s123456 LASTNAME FIRSTNAME
* s283816 Laiolo Marco

## Instructions

A general description of the BigLab 2 is avaible in the `course-materials` repository, [under _labs_](https://polito-wa1-aw1-2022.github.io/materials/labs/BigLab2/BigLab2.pdf). In the same repository, you can find the [instructions for GitHub Classroom](https://polito-wa1-aw1-2022.github.io/materials/labs/GH-Classroom-BigLab-Instructions.pdf), covering this and the next BigLab.

Once you cloned this repository, please write the group name and names of the members of the group in the above section.

In the `client` directory, do **NOT** create a new folder for the project, i.e., `client` should directly contain the `public` and `src` folders and the `package.json` files coming from BigLab1.

When committing on this repository, please, do **NOT** commit the `node_modules` directory, so that it is not pushed to GitHub.
This should be already automatically excluded from the `.gitignore` file, but please double-check.

When another member of the team pulls the updated project from the repository, remember to run `npm install` in the project directory to recreate all the Node.js dependencies locally, in the `node_modules` folder.
Remember that `npm install` should be executed inside the `client` and `server` folders (not in the `BigLab2` root directory).

Finally, remember to add the `final` tag for the final submission, otherwise it will not be graded.

## Registered Users

Here you can find a list of the users already registered inside the provided database. This information will be used during the fourth week, when you will have to deal with authentication.
If you decide to add additional users, please remember to add them to this table (with **plain-text password**)!

| email | password | name |
|-------|----------|------|
| john.doe@polito.it | password | John |
| mario.rossi@polito.it | password | Mario |
| root@polito.it | admin | Admin |
| gab.ian@polito.it | byte | Gabriele |

## List of APIs offered by the server

Provide a short description of the API you designed, with the required parameters. Please follow the proposed structure.

* [HTTP Method] [URL, with any parameter]
* [One-line about what this API is doing]
* [A (small) sample request, with body (if any)]
* [A (small) sample response, with body (if any)]
* [Error responses, if any]

# `server side`

The `server` is the server-side app companion of [`biglab2`](https://github.com/polito-AW1-2022-exams/biglab2-socket-close.git). It presents some APIs to perform CRUD operations on a film library.

## APIs
Hereafter, we report the designed HTTP APIs, also implemented in the project.

### __List Films using query parameters__

URL: `/api/films?filter=<filtername>&id=<id>`

Method: GET

Description: You can use query parameters to filter the data returned in endpoint responses. By specifying the `<id>` (optional) all filters will be ignored and you will only get the film with the given ID. Filters are optional if an `<id>` is specified.


| Filter Name | Response |
| --- | --- |
| _all_ | Get all the films in the library |
| _favorite_ | Get all films marked as favorite |
| _best_rated_ | Get all films with 5 stars rating |
| _seen_last_month_ | Get all films seen in the last month |
| _unseen_ | Get all unseen movies |


Request body: _None_

Response: `200 OK` (success), `500 Internal Server Error` (generic error) or `404 Not Found` (wrong ID or filter name).

Response body: An array of objects, each describing a film.
```
[{
    "id": 3,
    "title": "Star Wars",
    "favorite": 0,
    "watchdate": null,
    "rating": null,
}, {
    "id": 4,
    "title": "Matrix",
    "favorite": 0,
    "watchdate": null,
    "rating": null,
}
...
]
```

### __Get a Film (By ID)__

URL: `/api/films/<id>`

Method: GET

Description: Get the film identified by the id `<id>`.

Request body: _None_

Response: `200 OK` (success), `404 Not Found` (wrong code), or `500 Internal Server Error` (generic error).

Response body: An object, describing a single course.
```
{
    "code": "01TXYOV",
    "name": "Web Applications I",
    "CFU": 6
}
```

### __List Exams__

URL: `/api/exams`

Method: GET

Description: Get all the exams that the student already passed.

Request body: _None_

Response: `200 OK` (success) or `500 Internal Server Error` (generic error).

Response body: An array of objects, each describing an exam.
```
[{
    "code": "02LSEOV",
    "score": 25,
    "date": "2021-02-01"
},
...
]
```

### __Add a New Exam__

URL: `/api/exams`

Method: POST

Description: Add a new (passed) exam to the list of the student's exams.

Request body: An object representing an exam (Content-Type: `application/json`).
```
{
    "code": "01TXYOV",
    "score": 30,
    "date": "2021-05-04"
}
```

Response: `201 Created` (success) or `503 Service Unavailable` (generic error, e.g., when trying to insert an already existent exam). If the request body is not valid, `422 Unprocessable Entity` (validation error).

Response body: _None_

### __Update an Exam__

URL: `/api/exams/<code>`

Method: PUT

Description: Update entirely an existing (passed) exam, identified by its code.

Request body: An object representing the entire exam (Content-Type: `application/json`).
```
{
    "code": "01TXYOV",
    "score": 31,
    "date": "2021-05-04"
}
```

Response: `200 OK` (success) or `503 Service Unavailable` (generic error). If the request body is not valid, `422 Unprocessable Entity` (validation error).

Response body: _None_

### __Delete an Exam__

URL: `/api/exams/<code>`

Method: DELETE

Description: Delete an existing (passed) exam, identified by its code.

Request body: _None_

Response: `204 No Content` (success) or `503 Service Unavailable` (generic error).

Response body: _None_
