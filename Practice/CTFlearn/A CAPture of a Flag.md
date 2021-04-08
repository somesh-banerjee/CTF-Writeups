[**Problem**](https://ctflearn.com/challenge/356)

This one is a bit challenging as we have to use [wireshark](https://en.wikipedia.org/wiki/Wireshark) and I have never used it before.

- Open the file in wireshark.

- We know that http is used to send messages between two systems, so we apply the http filter and start seeing their info. You will get a mpacket with info "GET /?msg=......."

The message is base64 decrypted, encode it to get the flag.
