---
title: Openclarity
---

{{< blocks/cover title="Welcome to OpenClarity!" image_anchor="top" width="min" color="teal" >}}
<div class="mx-auto">
	<a class="btn btn-lg btn-primary mr-3 mb-4" href="{{< relref "/docs/" >}}">
		Learn More <i class="fa-solid fa-circle-right ml-2"></i>
	</a>
	<a class="btn btn-lg btn-secondary mr-3 mb-4" href="/docs/user-guide/">
		Install <i class="fa-brands fa-github ml-2 "></i>
	</a>
	<p class="lead mt-5">Open source tools for cloud native security and observability.</p>
</div>
{{< /blocks/cover >}}

{{% blocks/lead image_anchor="top" width="min" %}}
<div class="main-lead">
OpenClarity is a suite of open source tools for cloud native security and observability — VMClarity, KubeClarity, and APIClarity.
</div>
{{% /blocks/lead %}}

<section id="pageContent">
  <div class="container">
    <div class="card-deck">
      <div class="card">
        <img
          src="./img/logos/kube-clarity-android-chrome-192x192.png"
		  class="card-img-top"
		  draggable="false"
          style="padding: 2rem;"
          alt="KubeClarity logo"
        />
        <div class="card-body">
          <h5 class="card-title">KubeClarity</h5>
          <p class="card-text">
		  KubeClarity is a tool for detection and management of software bills of materials (SBOMs) and vulnerabilities in container images and filesystems. It scans both runtime Kubernetes clusters and CI/CD pipelines for enhanced software supply-chain security.
         </p>
        </div>
      </div>
      <div class="card">
        <img
          src="./img/logos/vm-clarity-android-chrome-192x192.png"
		  class="card-img-top"
		  draggable="false"
          style="padding: 2rem;"
          alt="VMClarity logo"
        />
        <div class="card-body">
          <h5 class="card-title">VMClarity</h5>
          <p class="card-text">
           VMClarity is an open source tool for agentless detection and management of Virtual Machine Software Bill Of Materials (SBOM) and security threats such as vulnerabilities, exploits, malware, rootkits, misconfigurations and leaked secrets.
          </p>
        </div>
      </div>
      <div class="card">
        <img
          src="./img/logos/api-clarity-android-chrome-192x192.png"
		  class="card-img-top"
		  draggable="false"
          style="padding: 2rem;"
          alt="APIClarity logo"
        />
        <div class="card-body">
          <h5 class="card-title">APIClarity</h5>
          <p class="card-text">
            APIClarity, an open source cloud native visibility tool for APIs, utilizes a service-mesh framework to capture and analyze API traffic, and identify potential risks.
          </p>
        </div>
      </div>
    </div>
</section>

{{% blocks/lead image_anchor="top" width="min" %}}
<div class="main-lead">Interested? Come join us on Slack or check out our Github page!</div>
{{% /blocks/lead %}}

{{< blocks/section color="light" type="row">}}
{{% blocks/feature icon="fa-lightbulb" title="Learn more about Openclarity!" url="/docs/" %}}
Read the Openclarity documentation.
{{% /blocks/feature %}}

{{% blocks/feature icon="fa-brands fa-github" title="Contributions welcome!" url="https://github.com/openclarity/" %}}
New users and developers are always welcome!
{{% /blocks/feature %}}

{{% blocks/feature icon="fa-brands fa-slack" title="Come chat with us!" url="https://outshift.slack.com/messages/vmclarity/" url_text="Join Slack" %}}
In case you need help, you can find us in our Slack channel.
{{% /blocks/feature %}}

{{< /blocks/section >}}
