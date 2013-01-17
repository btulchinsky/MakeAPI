# MakeAPI

## Running the Server

### Prerequisites

- [Redis](http://redis.io/)
- [MongoDB](http://www.mongodb.org/)
- [ElasticSearch](http://www.elasticsearch.org/)

### Dependencies

Execute `npm install` in the application directory:


### Running in Development mode

It's recommended that you use Foreman to run your development server. "Why?", you ask. Here's a great intro: [Introducing Foreman](http://blog.daviddollar.org/2011/05/06/introducing-foreman.html).

#### Configuration for Foreman

Copy and edit your .env file. -- This should never be committed to the repo.

```
cp .env.sample .env
```

#### Running the Services

There's a handy file named Procfile.services you can use to run Redis, ElasticSearch and MongoDB. To start all three services run:

```
foreman start -f Procfile.services
```

While either that is running, or the services are running independently, you can start the web server:

#### Running the Web Process

```
foreman start
```

By default the server will run at http://localhost:5000. You can change this by adding PORT=<port> to your .env file.


## Running the Tests

```
$ npm test
```

## API:

<table>
  <tr>
    <th>HTTP Method</th>
    <th>Path</th>
    <th>Action</th>
    <th>Notes</th>
  </tr>
  <tr>
    <th>POST</th>
    <td>api/make</td>
    <td>Create Make</td>
    <td>If Post Data is a valid Make, it creates one and returns it with the _id and __v populated.</td>
  </tr>
  <tr>
    <th>GET</th>
    <td>/api/make/:id</td>
    <td>Find a single Make</td>
    <td>Expects the last path element to be a valid ObjectId</td>
  </tr>
  <tr>
    <th>PUT</th>
    <td>/api/make/:id</td>
    <td>Update a Make</td>
    <td>The Make must already exist and the __v must be the same as the current version on the server. This is an implementation of optimistic locking.</td>
  </tr>
  <tr>
    <th>DELETE</th>
    <td>/api/make/:id</td>
    <td>Deletes a Make</td>
    <td>The effect is that of a delete operation, though the Make is actually only marked as deleted using the deletedAt timestamp.</td>
  </tr>
  <tr>
    <th>GET</th>
    <td>/api/makes</td>
    <td>Find All</td>
    <td><p>Finds all makes by default, can be used to filter and search.</p><p>TODO: Explain Search</p></td>
  </tr>
</table>


### Example Usage

```
  jQuery.ajax({
    type: "POST",
    url: "/api/make",
    data: {
      "url": "http://thimble.webmadecontent.org/abcd.html",
      "content-type": "text/html",
      "goal": "The goal of this lesson is to learn about img, p and blah tags...",
      "title": "Animal something-or-other",
      "locale": "en_us",
      "tags": ["awesome"],
      "privateTags": ["webmaker.org:project", "skill:css"],
      "description": "This handy HTML template makes it easy to quickly create your own text and image mashup, then publish it for sharing via Facebook, Tumblr or any web page. Your 15 seconds of internet fame await!"
      "author": "swex@mozilla.com",
      "contentAuthor": "swex@mozilla.com",
      "remixedFrom": null,
      "published": true
    },
    success: function(data, textStatus, jqXHR){
      console.log("Post resposne:");
      console.dir(data);
      console.log(textStatus);
      console.dir(jqXHR);
    },
    error: function(jqXHR, textStatus, errorThrown){
      console.log(jqXHR.responseText);
    }
  });
```


### A Playground

If you load http://localhost:5000/playground.html, you can use the loaded jQuery to interact with the API.