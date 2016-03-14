### Tracker

For each share
    - keep a list of active peers
    - keep a list of all chunks downloaded by peers
    - Respond to chunk requests. ie. when peer1 requests chunk#5, respond with list of peers that have chunk#5

### Registry

Make 
- Add share
- Search share

- p2pshare file format (filename.share)


- Client 
  - Search for share
  - Create a new share
    - reads filename.mp4
    - Make the json
    - Uploads to registry server

```json
{
    "id": 12,
    "filename": "filename.mp4",
    "hash": "{}md5hash}",
    "author": "{{ username }}",
    "chunks": [{
        "id": 1,
        "hash": "{{hash}}"
    },
    {
        "id": 2,
        "hash": "{{hash}}"
    },
    {
        "id": 3,
        "hash": "{{hash}}"
    },
    {
        "id": 4,
        "hash": "{{hash}}"
    }],
    "trackers": [
        "t1.p2pshare.net",
        "t2.p2pshare.net",
        "t3.p2pshare.net",
        "t4.p2pshare.net"
    ]
}
```

- trackers are decided by registry client

### Peer

```
peer start http://registry.p2pshare.net/12
```

- Downloads the share json with id 12. 
- Reads the metadata and chunk list from the json.
- Connects to one of the trackers and requests a chunk
- Gets reply with addresses of other peers with chunk
- Connects to a peer with with the chunk and downloads item
- Verfies the hash of the chunk
- When all chunks are received, stiches the file
- Also responds to chunk requests from other peers
