<a href="https://opensource.newrelic.com/oss-category/#new-relic-experimental"><picture><source media="(prefers-color-scheme: dark)" srcset="https://github.com/newrelic/opensource-website/raw/main/src/images/categories/dark/Experimental.png"><source media="(prefers-color-scheme: light)" srcset="https://github.com/newrelic/opensource-website/raw/main/src/images/categories/Experimental.png"><img alt="New Relic Open Source experimental project banner." src="https://github.com/newrelic/opensource-website/raw/main/src/images/categories/Experimental.png"></picture></a>

# newrelic-agent-operator
The <strong>newrelic-agent-operator</strong> is an implementation of the [Opentelemetry Operator](https://github.com/open-telemetry/opentelemetry-operator) that auto-instruments containerized workloads in Kubernetes with New Relic APM agents.

## Documentation

- [New Relic Agent Operator docs](./docs)

## Prerequisites

Currently, the New Relic Agent Operator requires [Cert Manager](https://cert-manager.io/docs/installation/) to be installed in your cluster.

## Helm Charts
You can install the New Relic Agent Operator via Helm from the newrelic-agent-operator repository.  Visit the [installation docs](./docs) for more info.

```
helm repo add newrelic-agent-operator https://newrelic-experimental.github.io/newrelic-agent-operator
helm upgrade --install newrelic-agent-operator newrelic-agent-operator/newrelic-agent-operator --set licenseKey='<NEW RELIC INGEST LICENSE KEY>' -n newrelic
```

## Building

1. Build and push your image to the location specified by `IMG`:

```sh
make container container-push  IMG=<some-registry>/newrelic-agent-operator:tag
```

2. Deploy the controller to the cluster with the image specified by `IMG`:

```sh
make deploy IMG=<some-registry>/newrelic-agent-operator:tag
```

### Uninstall CRDs
To delete the CRDs from the cluster:

```sh
make uninstall
```

### Undeploy controller
Undeploy the controller from the cluster:

```sh
make undeploy
```

### Test It Out
1. Install the CRDs into the cluster:

```sh
make install
```

2. Run your controller (this will run in the foreground, so switch to a new terminal if you want to leave it running):

```sh
make run
```

**NOTE:** You can also run this in one step by running: `make install run`

### Modifying the API definitions
If you are editing the API definitions, generate the manifests such as CRs or CRDs using:

```sh
make manifests
```

**NOTE:** Run `make --help` for more information on all potential `make` targets

More information can be found via the [Kubebuilder Documentation](https://book.kubebuilder.io/introduction.html)

## Things to consider
* Currently, <strong>newrelic-agent-operator</strong> supports instrumentation for [Python](https://docs.newrelic.com/docs/apm/agents/python-agent/configuration/python-agent-configuration/), [Java](https://docs.newrelic.com/docs/apm/agents/java-agent/getting-started/introduction-new-relic-java/), [Node.js](https://docs.newrelic.com/docs/apm/agents/nodejs-agent/getting-started/introduction-new-relic-nodejs/), [.NET](https://docs.newrelic.com/docs/apm/agents/net-agent/getting-started/introduction-new-relic-net/), and [Ruby](https://docs.newrelic.com/docs/apm/agents/ruby-agent/configuration/ruby-agent-configuration/).
* [cert-manager](https://cert-manager.io/docs/installation/) is required to be presented on cluster before starting newrelic-agent-operator


## Support

New Relic hosts and moderates an online forum where customers can interact with New Relic employees as well as other customers to get help and share best practices. If you're running into a problem, please raise an issue on this repository and we will try to help you ASAP. Please bear in mind this is an open source project and hence it isn't directly supported by New Relic.

## Contributing
We encourage your contributions to improve <strong>newrelic-agent-operator</strong> . Keep in mind when you submit your pull request, you'll need to sign the CLA via the click-through using CLA-Assistant. You only have to sign the CLA one time per project.
If you have any questions, or to execute our corporate CLA, required if your contribution is on behalf of a company,  please drop us an email at opensource@newrelic.com.

**A note about vulnerabilities**

As noted in our [security policy](../../security/policy), New Relic is committed to the privacy and security of our customers and their data. We believe that providing coordinated disclosure by security researchers and engaging with the security community are important means to achieve our security goals.

If you believe you have found a security vulnerability in this project or any of New Relic's products or websites, we welcome and greatly appreciate you reporting it to New Relic through [HackerOne](https://hackerone.com/newrelic).

## License
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
