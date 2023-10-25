---
---
1. Open an SSH tunnel to VMClarity the server

    ```shell
    ssh -N -L 8080:localhost:80 -i  "<Path to the SSH key specified during install>" ubuntu@<VmClarity SSH Address copied during install>
    ```

1. Open the VMClarity UI in your browser at [http://localhost:8080/](http://localhost:8080/). The dashboard opens.

    ![VMClarity UI Dashboard](/img/vmclarity-ui-1.png)

1. (Optional) If needed, you can access the API at[http://localhost:8080/api](http://localhost:8080/api). For details on the API, see {{% xref "/docs/vmclarity/api/_index.md" %}}.
