---
---
1. Open an SSH tunnel to VM Security the server

    ```shell
    ssh -N -L 8080:localhost:80 -i  "<Path to the SSH key specified during install>" ubuntu@<VmClarity SSH Address copied during install>
    ```

1. Open the VM Security UI in your browser at [http://localhost:8080/](http://localhost:8080/). The dashboard opens.

    ![VM Security UI Dashboard](/img/vmclarity-ui-1.png)

1. (Optional) If needed, you can access the API at[http://localhost:8080/api](http://localhost:8080/api). For details on the API, see {{% xref "/docs/vmclarity/api/_index.md" %}}.
