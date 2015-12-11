# Distributed Linkback Graph specification 0.1

This is a proposal for a system for publishing open data in an open, linked, collaborative and distributed manner.
It is a way for building a decentralized graph data store, that has pseudo-two-way links.
It is based on the Hypertext Transfer Protocol (HTTP) and Javascript Object Notation (JSON).

Distributed Linkback Graph (DLBG) works based on the following rules:

- The graph consists of Nodes and Links
- Each Node is identified by a URL
- A Node has: one value, an array of links, an array of linkbacks
- Links are typed one-way connections from one Node to another.
- Link types are a special kind of Node
- Nodes can (but are not required to) reciprocate a link through the linkback mechanism.

## Protocol

The protocol design is minimal, underspecified and 

### Node
Every Node is required to have the following requests:

**GET**

This will return a JSON object of the following format:
```json
{
  "DLBG": "0.1",
  "value": {value},
  "link": [
    {
      "href":"{url}",
      "type": "{url}"
    }
  ],
  "linkback":[
    {
      "href":"{url}",
      "type": "{url}"
    }
  ]
}
```

`Value` can be a String, Number, or Array. (Preferably not an Object)

**POST**
This will allow anyone to request a linkback on this Node. The post should be in this format:
```json
{
  "DLBG": "0.1",
  "href": "{url}",
  "type": "{url}"
}
```
The server will respond with the following:
```json
{
  "DLBG": "0.1",
  "message": "{received/accepted/rejected}"
}
```
### Linktype
**GET**
This will return a special Node that describes a link type. It does not have links or linkback
```json
{
  "DLBG": "0.1",
  "name": "{name}",
  "inverse": "{inverse name}",
  "description": "{short description}"
}
