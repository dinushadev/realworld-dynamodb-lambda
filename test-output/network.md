```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-g96vr@email.com",
    "username": "author-g96vr",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-g96vr@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1nOTZ2ciIsImlhdCI6MTU4NTI2NDA1NSwiZXhwIjoxNTg1NDM2ODU1fQ.JVDc-ThdehJC6-4Dn_rYkuA27z9HfoaFl9X9oWW9TIA",
    "username": "author-g96vr",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-6o2ivf@email.com",
    "username": "authoress-6o2ivf",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-6o2ivf@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy02bzJpdmYiLCJpYXQiOjE1ODUyNjQwNTUsImV4cCI6MTU4NTQzNjg1NX0.7cx73SH_fQh7wtCDhT5IVsUJxtoH32CgDtm2O1lvsmk",
    "username": "authoress-6o2ivf",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-wprzjl@email.com",
    "username": "non-author-wprzjl",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-wprzjl@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3Itd3ByempsIiwiaWF0IjoxNTg1MjY0MDU1LCJleHAiOjE1ODU0MzY4NTV9.qjzvaJ0m3Qh3cwJ4ZbMzXnd2WmZlEug2UtYeQkAAInk",
    "username": "non-author-wprzjl",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-nc57bl",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264055355,
    "updatedAt": 1585264055355,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-qqx8ry",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264055418,
    "updatedAt": 1585264055418,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-nc57bl
```
```
200 OK

{
  "article": {
    "createdAt": 1585264055355,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-nc57bl",
    "updatedAt": 1585264055355,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-qqx8ry
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1585264055418,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-qqx8ry",
    "updatedAt": 1585264055418,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/i0icbg
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [i0icbg]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-qqx8ry

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1585264055418,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-qqx8ry",
    "updatedAt": 1585264055418,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-qqx8ry

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1585264055418,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-qqx8ry",
    "updatedAt": 1585264055418,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-qqx8ry

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1585264055418,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-qqx8ry",
    "updatedAt": 1585264055418,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-qqx8ry

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-qqx8ry

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-qqx8ry

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-qqx8ry

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-qqx8ry]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-qqx8ry

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-g96vr]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-nc57bl/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1585264055355,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-nc57bl",
    "updatedAt": 1585264055355,
    "favoritedBy": [
      "non-author-wprzjl"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-nc57bl
```
```
200 OK

{
  "article": {
    "createdAt": 1585264055355,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-nc57bl",
    "updatedAt": 1585264055355,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-nc57bl/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-nc57bl_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-nc57bl_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-nc57bl/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1585264055355,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-nc57bl",
    "updatedAt": 1585264055355,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-nc57bl
```
```
200 OK

{}
```
```
GET /articles/title-nc57bl
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-nc57bl]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-qqx8ry
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-g96vr]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "kikl2r",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-m8nlj5",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056338,
    "updatedAt": 1585264056338,
    "author": {
      "username": "authoress-6o2ivf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "kikl2r",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "gm3n1v",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-u6kzfm",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056382,
    "updatedAt": 1585264056382,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "gm3n1v",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "koen0f",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-oghegd",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056411,
    "updatedAt": 1585264056411,
    "author": {
      "username": "authoress-6o2ivf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "koen0f",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "vkibo6",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-qio5q6",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056438,
    "updatedAt": 1585264056438,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "vkibo6",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "7jvp9r",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7x3qfj",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056463,
    "updatedAt": 1585264056463,
    "author": {
      "username": "authoress-6o2ivf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "7jvp9r",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "r3tb6w",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mwznn7",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056489,
    "updatedAt": 1585264056489,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "r3tb6w",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "jzmdzk",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-gvb2q9",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056515,
    "updatedAt": 1585264056515,
    "author": {
      "username": "authoress-6o2ivf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "jzmdzk",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "8y4hqw",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-4qwj5x",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056539,
    "updatedAt": 1585264056539,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "8y4hqw",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "z5rh26",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ym1iox",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056565,
    "updatedAt": 1585264056565,
    "author": {
      "username": "authoress-6o2ivf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "z5rh26",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "sjcxqd",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-hhcsym",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056595,
    "updatedAt": 1585264056595,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "sjcxqd",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "b6owbp",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-n6gek4",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056627,
    "updatedAt": 1585264056627,
    "author": {
      "username": "authoress-6o2ivf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "b6owbp",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "i8z7xe",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-junfyy",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056661,
    "updatedAt": 1585264056661,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "i8z7xe",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ehcj01",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-exf805",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056684,
    "updatedAt": 1585264056684,
    "author": {
      "username": "authoress-6o2ivf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ehcj01",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "jop50c",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-p9vypp",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056710,
    "updatedAt": 1585264056710,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "jop50c",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "522kp8",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-eve1ir",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056735,
    "updatedAt": 1585264056735,
    "author": {
      "username": "authoress-6o2ivf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "522kp8",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "vyg4at",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mex8al",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056764,
    "updatedAt": 1585264056764,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "vyg4at",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "jvp5f1",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-1i3r86",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056789,
    "updatedAt": 1585264056789,
    "author": {
      "username": "authoress-6o2ivf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "jvp5f1",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "6fdcnk",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-b58vdb",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056816,
    "updatedAt": 1585264056816,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "6fdcnk",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "ia9zum",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-lfmreg",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056840,
    "updatedAt": 1585264056840,
    "author": {
      "username": "authoress-6o2ivf",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "ia9zum",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "go2v4f",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-c9jvhg",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264056880,
    "updatedAt": 1585264056880,
    "author": {
      "username": "author-g96vr",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "go2v4f",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "go2v4f",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056880,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c9jvhg",
      "updatedAt": 1585264056880,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ia9zum",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056840,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lfmreg",
      "updatedAt": 1585264056840,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6fdcnk",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056816,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b58vdb",
      "updatedAt": 1585264056816,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jvp5f1",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056789,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1i3r86",
      "updatedAt": 1585264056789,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "vyg4at"
      ],
      "createdAt": 1585264056764,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mex8al",
      "updatedAt": 1585264056764,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "522kp8",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056735,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eve1ir",
      "updatedAt": 1585264056735,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jop50c",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056710,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9vypp",
      "updatedAt": 1585264056710,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ehcj01",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056684,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-exf805",
      "updatedAt": 1585264056684,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i8z7xe",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056661,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-junfyy",
      "updatedAt": 1585264056661,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "b6owbp",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056627,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-n6gek4",
      "updatedAt": 1585264056627,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "sjcxqd",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056595,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hhcsym",
      "updatedAt": 1585264056595,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "z5rh26"
      ],
      "createdAt": 1585264056565,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ym1iox",
      "updatedAt": 1585264056565,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8y4hqw",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056539,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4qwj5x",
      "updatedAt": 1585264056539,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jzmdzk",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056515,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gvb2q9",
      "updatedAt": 1585264056515,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r3tb6w",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056489,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mwznn7",
      "updatedAt": 1585264056489,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7jvp9r",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056463,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7x3qfj",
      "updatedAt": 1585264056463,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "vkibo6"
      ],
      "createdAt": 1585264056438,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qio5q6",
      "updatedAt": 1585264056438,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "koen0f",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056411,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oghegd",
      "updatedAt": 1585264056411,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gm3n1v",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056382,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-u6kzfm",
      "updatedAt": 1585264056382,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kikl2r",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056338,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m8nlj5",
      "updatedAt": 1585264056338,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "8y4hqw",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056539,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4qwj5x",
      "updatedAt": 1585264056539,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "6fdcnk",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056816,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b58vdb",
      "updatedAt": 1585264056816,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "522kp8",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056735,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eve1ir",
      "updatedAt": 1585264056735,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i8z7xe",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056661,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-junfyy",
      "updatedAt": 1585264056661,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "z5rh26"
      ],
      "createdAt": 1585264056565,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ym1iox",
      "updatedAt": 1585264056565,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r3tb6w",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056489,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mwznn7",
      "updatedAt": 1585264056489,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "koen0f",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056411,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oghegd",
      "updatedAt": 1585264056411,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-6o2ivf
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "ia9zum",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056840,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lfmreg",
      "updatedAt": 1585264056840,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jvp5f1",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056789,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1i3r86",
      "updatedAt": 1585264056789,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "522kp8",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056735,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eve1ir",
      "updatedAt": 1585264056735,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ehcj01",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056684,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-exf805",
      "updatedAt": 1585264056684,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "b6owbp",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056627,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-n6gek4",
      "updatedAt": 1585264056627,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "z5rh26"
      ],
      "createdAt": 1585264056565,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ym1iox",
      "updatedAt": 1585264056565,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jzmdzk",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056515,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gvb2q9",
      "updatedAt": 1585264056515,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7jvp9r",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056463,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7x3qfj",
      "updatedAt": 1585264056463,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "koen0f",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056411,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oghegd",
      "updatedAt": 1585264056411,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kikl2r",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056338,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m8nlj5",
      "updatedAt": 1585264056338,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-wprzjl
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-g96vr&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "go2v4f",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056880,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c9jvhg",
      "updatedAt": 1585264056880,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6fdcnk",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056816,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b58vdb",
      "updatedAt": 1585264056816,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-g96vr&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "vyg4at"
      ],
      "createdAt": 1585264056764,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mex8al",
      "updatedAt": 1585264056764,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jop50c",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056710,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9vypp",
      "updatedAt": 1585264056710,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "go2v4f",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056880,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c9jvhg",
      "updatedAt": 1585264056880,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ia9zum",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056840,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lfmreg",
      "updatedAt": 1585264056840,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6fdcnk",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056816,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b58vdb",
      "updatedAt": 1585264056816,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jvp5f1",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056789,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1i3r86",
      "updatedAt": 1585264056789,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "vyg4at"
      ],
      "createdAt": 1585264056764,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mex8al",
      "updatedAt": 1585264056764,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "522kp8",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056735,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eve1ir",
      "updatedAt": 1585264056735,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jop50c",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056710,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9vypp",
      "updatedAt": 1585264056710,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ehcj01",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056684,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-exf805",
      "updatedAt": 1585264056684,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i8z7xe",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056661,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-junfyy",
      "updatedAt": 1585264056661,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "b6owbp",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056627,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-n6gek4",
      "updatedAt": 1585264056627,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "sjcxqd",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056595,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hhcsym",
      "updatedAt": 1585264056595,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "z5rh26"
      ],
      "createdAt": 1585264056565,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ym1iox",
      "updatedAt": 1585264056565,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8y4hqw",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056539,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4qwj5x",
      "updatedAt": 1585264056539,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jzmdzk",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056515,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gvb2q9",
      "updatedAt": 1585264056515,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r3tb6w",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056489,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mwznn7",
      "updatedAt": 1585264056489,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7jvp9r",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056463,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7x3qfj",
      "updatedAt": 1585264056463,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "vkibo6"
      ],
      "createdAt": 1585264056438,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qio5q6",
      "updatedAt": 1585264056438,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "koen0f",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056411,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oghegd",
      "updatedAt": 1585264056411,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gm3n1v",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056382,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-u6kzfm",
      "updatedAt": 1585264056382,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kikl2r",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056338,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m8nlj5",
      "updatedAt": 1585264056338,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-6o2ivf/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-6o2ivf",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "ia9zum",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056840,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lfmreg",
      "updatedAt": 1585264056840,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jvp5f1",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056789,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1i3r86",
      "updatedAt": 1585264056789,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "522kp8",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056735,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eve1ir",
      "updatedAt": 1585264056735,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ehcj01",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056684,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-exf805",
      "updatedAt": 1585264056684,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "b6owbp",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056627,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-n6gek4",
      "updatedAt": 1585264056627,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "z5rh26"
      ],
      "createdAt": 1585264056565,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ym1iox",
      "updatedAt": 1585264056565,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jzmdzk",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056515,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gvb2q9",
      "updatedAt": 1585264056515,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7jvp9r",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056463,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7x3qfj",
      "updatedAt": 1585264056463,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "koen0f",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056411,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oghegd",
      "updatedAt": 1585264056411,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kikl2r",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056338,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m8nlj5",
      "updatedAt": 1585264056338,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-g96vr/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-g96vr",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "go2v4f",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056880,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c9jvhg",
      "updatedAt": 1585264056880,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ia9zum",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056840,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lfmreg",
      "updatedAt": 1585264056840,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "6fdcnk",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056816,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-b58vdb",
      "updatedAt": 1585264056816,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jvp5f1",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056789,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-1i3r86",
      "updatedAt": 1585264056789,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "vyg4at"
      ],
      "createdAt": 1585264056764,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mex8al",
      "updatedAt": 1585264056764,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "522kp8",
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056735,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-eve1ir",
      "updatedAt": 1585264056735,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jop50c",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056710,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-p9vypp",
      "updatedAt": 1585264056710,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "ehcj01",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056684,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-exf805",
      "updatedAt": 1585264056684,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "i8z7xe",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056661,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-junfyy",
      "updatedAt": 1585264056661,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "b6owbp",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056627,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-n6gek4",
      "updatedAt": 1585264056627,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "sjcxqd",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056595,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-hhcsym",
      "updatedAt": 1585264056595,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "z5rh26"
      ],
      "createdAt": 1585264056565,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ym1iox",
      "updatedAt": 1585264056565,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "8y4hqw",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056539,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4qwj5x",
      "updatedAt": 1585264056539,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "jzmdzk",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056515,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-gvb2q9",
      "updatedAt": 1585264056515,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r3tb6w",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056489,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mwznn7",
      "updatedAt": 1585264056489,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "7jvp9r",
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056463,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7x3qfj",
      "updatedAt": 1585264056463,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0",
        "vkibo6"
      ],
      "createdAt": 1585264056438,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qio5q6",
      "updatedAt": 1585264056438,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "koen0f",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1585264056411,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-oghegd",
      "updatedAt": 1585264056411,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gm3n1v",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1585264056382,
      "author": {
        "username": "author-g96vr",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-u6kzfm",
      "updatedAt": 1585264056382,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kikl2r",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1585264056338,
      "author": {
        "username": "authoress-6o2ivf",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-m8nlj5",
      "updatedAt": 1585264056338,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "kikl2r",
    "tag_0",
    "tag_mod_2_0",
    "tag_mod_3_0",
    "sjcxqd",
    "tag_9",
    "tag_mod_2_1",
    "tag_a",
    "tag_b",
    "6fdcnk",
    "tag_17",
    "tag_mod_3_2",
    "go2v4f",
    "tag_19",
    "tag_mod_3_1",
    "jvp5f1",
    "tag_16",
    "jop50c",
    "tag_13",
    "ehcj01",
    "tag_12",
    "522kp8",
    "tag_14",
    "jzmdzk",
    "tag_6",
    "tag_3",
    "vkibo6",
    "gm3n1v",
    "tag_1",
    "i8z7xe",
    "tag_11",
    "b6owbp",
    "tag_10",
    "koen0f",
    "tag_2",
    "r3tb6w",
    "tag_5",
    "tag_8",
    "z5rh26",
    "ia9zum",
    "tag_18",
    "7jvp9r",
    "tag_4",
    "tag_15",
    "vyg4at",
    "8y4hqw",
    "tag_7"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author--z2oro4@email.com",
    "username": "author--z2oro4",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author--z2oro4@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci0tejJvcm80IiwiaWF0IjoxNTg1MjY0MDU4LCJleHAiOjE1ODU0MzY4NTh9.2VcEw_-w7flmRbPxdgr5ziQd0KKxg_VHrfzr-VAkszg",
    "username": "author--z2oro4",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-gv4rc@email.com",
    "username": "commenter-gv4rc",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-gv4rc@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1ndjRyYyIsImlhdCI6MTU4NTI2NDA1OCwiZXhwIjoxNTg1NDM2ODU4fQ._gMmoQjPfaQy2uD3aKfZtISPPCVSv8Y-Oh84nHTKfoM",
    "username": "commenter-gv4rc",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-nmpxq5",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1585264058391,
    "updatedAt": 1585264058391,
    "author": {
      "username": "author--z2oro4",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-nmpxq5/comments

{
  "comment": {
    "body": "test comment i0m06v"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "9226434c-49df-470f-8145-1ce43239bc45",
    "slug": "title-nmpxq5",
    "body": "test comment i0m06v",
    "createdAt": 1585264058424,
    "updatedAt": 1585264058424,
    "author": {
      "username": "commenter-gv4rc",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nmpxq5/comments

{
  "comment": {
    "body": "test comment ysvg1u"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "44e98bb5-e5d6-4b7a-9437-da6a32bd3420",
    "slug": "title-nmpxq5",
    "body": "test comment ysvg1u",
    "createdAt": 1585264058456,
    "updatedAt": 1585264058456,
    "author": {
      "username": "commenter-gv4rc",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nmpxq5/comments

{
  "comment": {
    "body": "test comment npkcj"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "e3ffdc96-6c1c-4cba-8cf6-5428d96b6313",
    "slug": "title-nmpxq5",
    "body": "test comment npkcj",
    "createdAt": 1585264058492,
    "updatedAt": 1585264058492,
    "author": {
      "username": "commenter-gv4rc",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nmpxq5/comments

{
  "comment": {
    "body": "test comment y1qn3m"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "7516fae0-5bf5-4e30-a2e5-9eba5211694f",
    "slug": "title-nmpxq5",
    "body": "test comment y1qn3m",
    "createdAt": 1585264058521,
    "updatedAt": 1585264058521,
    "author": {
      "username": "commenter-gv4rc",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nmpxq5/comments

{
  "comment": {
    "body": "test comment te1ash"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "1cd3d48f-787d-4948-afa7-4965c8891fb1",
    "slug": "title-nmpxq5",
    "body": "test comment te1ash",
    "createdAt": 1585264058552,
    "updatedAt": 1585264058552,
    "author": {
      "username": "commenter-gv4rc",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nmpxq5/comments

{
  "comment": {
    "body": "test comment f1luxs"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "2a440fd9-449f-4d1d-a019-69e856c1e6a7",
    "slug": "title-nmpxq5",
    "body": "test comment f1luxs",
    "createdAt": 1585264058576,
    "updatedAt": 1585264058576,
    "author": {
      "username": "commenter-gv4rc",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nmpxq5/comments

{
  "comment": {
    "body": "test comment wnk7ey"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "445cba86-e178-4835-832c-8c162ba5b241",
    "slug": "title-nmpxq5",
    "body": "test comment wnk7ey",
    "createdAt": 1585264058606,
    "updatedAt": 1585264058606,
    "author": {
      "username": "commenter-gv4rc",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nmpxq5/comments

{
  "comment": {
    "body": "test comment sk3wh0"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "d125aa64-1255-4249-881c-8da24d5d1a58",
    "slug": "title-nmpxq5",
    "body": "test comment sk3wh0",
    "createdAt": 1585264058636,
    "updatedAt": 1585264058636,
    "author": {
      "username": "commenter-gv4rc",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nmpxq5/comments

{
  "comment": {
    "body": "test comment i3ydwq"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "cb9a1366-e3c2-488e-8741-6f53acacaab9",
    "slug": "title-nmpxq5",
    "body": "test comment i3ydwq",
    "createdAt": 1585264058672,
    "updatedAt": 1585264058672,
    "author": {
      "username": "commenter-gv4rc",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-nmpxq5/comments

{
  "comment": {
    "body": "test comment lqk922"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "00fd0af0-81ee-409b-bb23-103b89a0eb5d",
    "slug": "title-nmpxq5",
    "body": "test comment lqk922",
    "createdAt": 1585264058708,
    "updatedAt": 1585264058708,
    "author": {
      "username": "commenter-gv4rc",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-nmpxq5/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-nmpxq5/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment caa45k"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-nmpxq5/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1585264058456,
      "id": "44e98bb5-e5d6-4b7a-9437-da6a32bd3420",
      "body": "test comment ysvg1u",
      "slug": "title-nmpxq5",
      "author": {
        "username": "commenter-gv4rc",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585264058456
    },
    {
      "createdAt": 1585264058708,
      "id": "00fd0af0-81ee-409b-bb23-103b89a0eb5d",
      "body": "test comment lqk922",
      "slug": "title-nmpxq5",
      "author": {
        "username": "commenter-gv4rc",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585264058708
    },
    {
      "createdAt": 1585264058672,
      "id": "cb9a1366-e3c2-488e-8741-6f53acacaab9",
      "body": "test comment i3ydwq",
      "slug": "title-nmpxq5",
      "author": {
        "username": "commenter-gv4rc",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585264058672
    },
    {
      "createdAt": 1585264058606,
      "id": "445cba86-e178-4835-832c-8c162ba5b241",
      "body": "test comment wnk7ey",
      "slug": "title-nmpxq5",
      "author": {
        "username": "commenter-gv4rc",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585264058606
    },
    {
      "createdAt": 1585264058576,
      "id": "2a440fd9-449f-4d1d-a019-69e856c1e6a7",
      "body": "test comment f1luxs",
      "slug": "title-nmpxq5",
      "author": {
        "username": "commenter-gv4rc",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585264058576
    },
    {
      "createdAt": 1585264058636,
      "id": "d125aa64-1255-4249-881c-8da24d5d1a58",
      "body": "test comment sk3wh0",
      "slug": "title-nmpxq5",
      "author": {
        "username": "commenter-gv4rc",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585264058636
    },
    {
      "createdAt": 1585264058521,
      "id": "7516fae0-5bf5-4e30-a2e5-9eba5211694f",
      "body": "test comment y1qn3m",
      "slug": "title-nmpxq5",
      "author": {
        "username": "commenter-gv4rc",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585264058521
    },
    {
      "createdAt": 1585264058424,
      "id": "9226434c-49df-470f-8145-1ce43239bc45",
      "body": "test comment i0m06v",
      "slug": "title-nmpxq5",
      "author": {
        "username": "commenter-gv4rc",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585264058424
    },
    {
      "createdAt": 1585264058492,
      "id": "e3ffdc96-6c1c-4cba-8cf6-5428d96b6313",
      "body": "test comment npkcj",
      "slug": "title-nmpxq5",
      "author": {
        "username": "commenter-gv4rc",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585264058492
    },
    {
      "createdAt": 1585264058552,
      "id": "1cd3d48f-787d-4948-afa7-4965c8891fb1",
      "body": "test comment te1ash",
      "slug": "title-nmpxq5",
      "author": {
        "username": "commenter-gv4rc",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1585264058552
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-nmpxq5/comments/9226434c-49df-470f-8145-1ce43239bc45
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-nmpxq5/comments/44e98bb5-e5d6-4b7a-9437-da6a32bd3420
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-gv4rc]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-nmpxq5/comments/44e98bb5-e5d6-4b7a-9437-da6a32bd3420
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-nmpxq5/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.x0alkraff5@email.com",
    "username": "user1-0.x0alkraff5",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.x0alkraff5@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAueDBhbGtyYWZmNSIsImlhdCI6MTU4NTI2NDA1OCwiZXhwIjoxNTg1NDM2ODU4fQ.fyUpgatAQ8n1-MnSbGMkmqebQ02-EBYad1yexn9kXdA",
    "username": "user1-0.x0alkraff5",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.x0alkraff5@email.com",
    "username": "user1-0.x0alkraff5",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.x0alkraff5]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.x0alkraff5@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.x0alkraff5@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.x0alkraff5@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.x0alkraff5@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAueDBhbGtyYWZmNSIsImlhdCI6MTU4NTI2NDA1OSwiZXhwIjoxNTg1NDM2ODU5fQ.usuMuAvmuLMVSzeA9sVMfgBNhHKtWdwvZxa5RkpPA5E",
    "username": "user1-0.x0alkraff5",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.y60rltzj95",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.y60rltzj95]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.x0alkraff5@email.com",
    "password": "0.ya7ejh2lh3"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.x0alkraff5@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAueDBhbGtyYWZmNSIsImlhdCI6MTU4NTI2NDA1OSwiZXhwIjoxNTg1NDM2ODU5fQ.usuMuAvmuLMVSzeA9sVMfgBNhHKtWdwvZxa5RkpPA5E",
    "username": "user1-0.x0alkraff5",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.x0alkraff5
```
```
200 OK

{
  "profile": {
    "username": "user1-0.x0alkraff5",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.qdn9gxy5p4b
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.qdn9gxy5p4b]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1ODUyNjQwNTksImV4cCI6MTU4NTQzNjg1OX0.-DR3tOAi2z8LstydEVSmepoBcocQbEaeR9DBgs3mJWc",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.nhkjkxsxq5a",
    "email": "user2-0.nhkjkxsxq5a@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.nhkjkxsxq5a@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAubmhramt4c3hxNWEiLCJpYXQiOjE1ODUyNjQwNTksImV4cCI6MTU4NTQzNjg1OX0.dPWcXdegDzr3bwSBu9hI0kz2qbo2EIRJPvi_skCQbpw",
    "username": "user2-0.nhkjkxsxq5a",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.x0alkraff5@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.x0alkraff5",
    "email": "updated-user1-0.x0alkraff5@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAueDBhbGtyYWZmNSIsImlhdCI6MTU4NTI2NDA1OSwiZXhwIjoxNTg1NDM2ODU5fQ.usuMuAvmuLMVSzeA9sVMfgBNhHKtWdwvZxa5RkpPA5E"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.x0alkraff5",
    "email": "updated-user1-0.x0alkraff5@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAueDBhbGtyYWZmNSIsImlhdCI6MTU4NTI2NDA1OSwiZXhwIjoxNTg1NDM2ODU5fQ.usuMuAvmuLMVSzeA9sVMfgBNhHKtWdwvZxa5RkpPA5E"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.x0alkraff5",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAueDBhbGtyYWZmNSIsImlhdCI6MTU4NTI2NDA1OSwiZXhwIjoxNTg1NDM2ODU5fQ.usuMuAvmuLMVSzeA9sVMfgBNhHKtWdwvZxa5RkpPA5E"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.x0alkraff5",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAueDBhbGtyYWZmNSIsImlhdCI6MTU4NTI2NDA1OSwiZXhwIjoxNTg1NDM2ODU5fQ.usuMuAvmuLMVSzeA9sVMfgBNhHKtWdwvZxa5RkpPA5E"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.79yeceow98u@email.com",
    "username": "user2-0.79yeceow98u",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.79yeceow98u@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuNzl5ZWNlb3c5OHUiLCJpYXQiOjE1ODUyNjQwNTksImV4cCI6MTU4NTQzNjg1OX0.MbjKlcM8BG05YD43SNR5KfzCnkznmVSS-e3FeAZa-z8",
    "username": "user2-0.79yeceow98u",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.79yeceow98u@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.79yeceow98u@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2020-03-26T23:07:39.713Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
