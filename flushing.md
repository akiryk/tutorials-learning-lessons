# Flushing

The idea is for the server to send something to the client as quickly as possible, even — or especially — if there is still a lot work to be done. This "something", called a chunk, can be parsed and displayed by the browser while the server is still doing other work. That process is called "early flushing."

Ideally, if you early flush, you'd send down under 14kb of data so as to fit in the [TCP Congestion Window](https://en.wikipedia.org/wiki/TCP_congestion_control#Congestion_window). Additional chunks can be sent down when ready — the browser can handle it using the [chunked transfer encoding](https://en.wikipedia.org/wiki/Chunked_transfer_encoding) protocol, which is a feature of http.

