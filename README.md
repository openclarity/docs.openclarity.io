# docs.openclarity.io

[![Netlify Status](https://api.netlify.com/api/v1/badges/59e14813-c990-41a0-8662-45c204e6bc6b/deploy-status)](https://app.netlify.com/sites/hugo-openclarity/deploys)

Openclarity documentation portal based on Hugo and Docsy

[Docsy][] is a [Hugo theme module][] for technical documentation sites, providing easy
site navigation, structure, and more. This **Docsy Example Project** uses the Docsy
theme component as a hugo module and provides a skeleton documentation structure for you to use.
You can clone/copy this project and edit it with your own content, or use it as an example.

In this project, the Docsy theme component is pulled in as a Hugo module, together with other module dependencies:

```console
$ hugo mod graph
hugo: collected modules in 566 ms
hugo: collected modules in 578 ms
github.com/google/docsy-example github.com/google/docsy@v0.7.1
github.com/google/docsy-example github.com/google/docsy/dependencies@v0.7.1
github.com/google/docsy/dependencies@v0.7.1 github.com/twbs/bootstrap@v5.2.3+incompatible
github.com/google/docsy/dependencies@v0.7.1 github.com/FortAwesome/Font-Awesome@v0.0.0-20230327165841-0698449d50f2
```

You can find detailed theme instructions in the [Docsy user guide][].

## Running the website locally

Building and running the site locally requires a recent `extended` version of [Hugo](https://gohugo.io).
You can find out more about how to install Hugo for your environment in our
[Getting started](https://www.docsy.dev/docs/getting-started/#prerequisites-and-installation) guide.

Once you've made your working copy of the site repo, from the repo root folder, run:

```bash
hugo server
```

## Troubleshooting

As you run the website locally, you may run into the following error:

```console
$ hugo server
WARN 2023/06/27 16:59:06 Module "project" is not compatible with this Hugo version; run "hugo mod graph" for more information.
Start building sites …
hugo v0.101.0-466fa43c16709b4483689930a4f9ac8add5c9f66+extended windows/amd64 BuildDate=2022-06-16T07:09:16Z VendorInfo=gohugoio
Error: Error building site: "C:\Users\foo\path\to\docsy-example\content\en\_index.md:5:1": failed to extract shortcode: template for shortcode "blocks/cover" not found
Built in 27 ms
```

This error occurs if you are running an outdated version of Hugo. As of docsy theme version `v0.7.0`, hugo version `0.110.0` or higher is required.
See this [section](https://www.docsy.dev/docs/get-started/docsy-as-module/installation-prerequisites/#install-hugo) of the user guide for instructions on how to install Hugo.

Or you may be confronted with the following error:

```console
$ hugo server

INFO 2021/01/21 21:07:55 Using config file:
Building sites … INFO 2021/01/21 21:07:55 syncing static files to /
Built in 288 ms
Error: Error building site: TOCSS: failed to transform "scss/main.scss" (text/x-scss): resource "scss/scss/main.scss_9fadf33d895a46083cdd64396b57ef68" not found in file cache
```

This error occurs if you have not installed the extended version of Hugo.
See this [section](https://www.docsy.dev/docs/get-started/docsy-as-module/installation-prerequisites/#install-hugo) of the user guide for instructions on how to install Hugo.

Or you may encounter the following error:

```console
$ hugo server

Error: failed to download modules: binary with name "go" not found
```

This error occurs if you have not installed the `go` programming language on your system.
See this [section](https://www.docsy.dev/docs/get-started/docsy-as-module/installation-prerequisites/#install-go-language) of the user guide for instructions on how to install `go`.

[Docsy user guide]: https://docsy.dev/docs
[Docsy]: https://github.com/google/docsy
[Hugo theme module]: https://gohugo.io/hugo-modules/use-modules/#use-a-module-for-a-theme