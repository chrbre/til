# Using json server

https://www.npmjs.com/package/json-server

JSON Server ist ein lokaler JSON server, der ein JSON file als REST Service zur Verfügung stellt. Man kann ihn als npm package installieren, oder aber man startet ihn einfach mit:

```bash
npx json-server --watch {patch_to_json_file} --port {port}
```

Man liegt seine JSON Daten in ein File, das verschiedene Arrays auf der root Ebene enthält. z.b.

```bash
{
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```

Die Elemente auf der root Ebene werden dabei als Ressourcen interpretiert und können mit REST calls beeinflußt werden

```bash
GET    /posts
GET    /posts/1
POST   /posts
PUT    /posts/1
PATCH  /posts/1
DELETE /posts/1
```

Es können auch Objekte statt Arrays beeinflußt werden.
