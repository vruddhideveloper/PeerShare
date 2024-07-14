### PeerShare

**Multithreaded Peer-to-Peer File Sharing using Socket Programming**

Developed a peer-to-peer network for file sharing, drawing inspiration from BitTorrent but with reduced complexity. The network consists of two main components: peers and a file owner. The file owner holds a file, splits it into 100KB chunks, and stores each chunk as an individual file. The file owner listens on a TCP port, acting as a multithreaded server capable of serving multiple clients at once.

#### Project Specifications

Each peer connects to the file owner to download chunks. Peers have two threads: one serves as a server to upload local chunks to another peer (the upload neighbor), and the other functions as a client to download chunks from a different peer (the download neighbor). Consequently, each peer has two neighbors: one from which it downloads chunks and another to which it uploads chunks. Any peer can directly connect to any other peer.

#### Procedure

1. Launch the file owner process, specifying a listening port.
2. Sequentially start five peer processes, providing each with the file owner's port, the peer's own listening port, and its download neighbor's port.
3. Each peer connects to the file owner's port. The file owner then creates a new thread to send one or more chunks to the peer, while the main thread continues to listen for new connections.
4. After obtaining chunks from the file owner, the peer saves them as individual files and generates a summary file listing the IDs of the chunks it has.
5. The peer then spawns two new threads: one to handle upload requests from its upload neighbor and the other to connect to its download neighbor.
6. The peer requests the chunk ID list from its download neighbor, compares it with its own list to identify missing chunks, and requests a missing chunk. Concurrently, it sends its chunk ID list to the upload neighbor and uploads chunks as requested.
7. When a peer collects all file chunks, it assembles them into a single file.
8. A peer must log its activities to the console, including when it receives or sends a chunk, exchanges chunk ID lists, requests chunks, or handles such requests.
