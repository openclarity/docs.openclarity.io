---
---
Open an SSH tunnel to VMClarity the server

```shell
ssh -N -L 8080:localhost:80 -i  "<Path to the SSH key specified during install>" ubuntu@<VmClarity SSH Address copied during install>
```
