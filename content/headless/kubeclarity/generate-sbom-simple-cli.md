---
---
To generate the Software Bill of Materials (SBOM), complete the following steps.

1. Run the following command.

    ```shell
    kubeclarity-cli analyze <image/directory name> --input-type <dir|file|image(default)> -o <output file or stdout>
    ```

    For example:

    ```shell
    kubeclarity-cli analyze --input-type image nginx:latest -o nginx.sbom
    ```

    Example output:

    ```shell
    INFO[0000] Called syft analyzer on source registry:nginx:latest  analyzer=syft app=kubeclarity
    INFO[0004] Skipping analyze unsupported source type: image  analyzer=gomod app=kubeclarity
    INFO[0004] Sending successful results                    analyzer=syft app=kubeclarity
    INFO[0004] Got result for job "syft"                     app=kubeclarity
    INFO[0004] Got result for job "gomod"                    app=kubeclarity
    INFO[0004] Skip generating hash in the case of image    
    ```

1. Verify that the `ngnix.sbom` file is generated and explore its contents as in below:

    ```shell
    head ngnix.sbom
    ```

    Example output:

    ```yaml
    {
      "bomFormat": "CycloneDX",
      "specVersion": "1.4",
      "serialNumber": "urn:uuid:8cca2aa3-1aaa-4e8c-9d44-08e88b1df50d",
      "version": 1,
      "metadata": {
        "timestamp": "2023-05-19T16:27:27-07:00",
        "tools": [
          {
            "vendor": "kubeclarity",
    ```

1. To run also the trivy scanner and merge the output into a single SBOM, run:

    ```shell
    ANALYZER_LIST="syft gomod trivy" kubeclarity-cli analyze --input-type image nginx:latest -o nginx.sbom
    ```

    Example output:

    ```shell
    INFO[0000] Called syft analyzer on source registry:nginx:latest  analyzer=syft app=kubeclarity
    INFO[0004] Called trivy analyzer on source image nginx:latest  analyzer=trivy app=kubeclarity
    INFO[0004] Skipping analyze unsupported source type: image  analyzer=gomod app=kubeclarity
    INFO[0005] Sending successful results                    analyzer=syft app=kubeclarity
    INFO[0005] Sending successful results                    analyzer=trivy app=kubeclarity
    INFO[0005] Got result for job "trivy"                    app=kubeclarity
    INFO[0005] Got result for job "syft"                     app=kubeclarity
    INFO[0005] Got result for job "gomod"                    app=kubeclarity
    INFO[0005] Skip generating hash in the case of image   
    ```
