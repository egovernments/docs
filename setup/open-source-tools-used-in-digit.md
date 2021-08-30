---
description: Overall tool stack used in DIGIT
---

# Open Source Tools used in DIGIT

DIGIT being an open source platform, all the tools and tech stack used to build, deploy and operate DIGIT - are also [open source](https://opensource.com/resources/what-open-source) and community edition. All the various tools used are listed below with the specific versions used and their short description.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Platform Tools</th>
      <th style="text-align:left">Latest Version</th>
      <th style="text-align:left">Used Version</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">License Type</th>
      <th style="text-align:left">&#x200B;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://dattell.com/data-architecture-blog/comparing-confluent-kafka-and-apache-kafka/">Confluent Kafka</a>&#x200B;</td>
      <td
      style="text-align:left">6.2.0</td>
        <td style="text-align:left">5.4.1</td>
        <td style="text-align:left">Apache <b>Kafka</b> is a open sourced and community distributed event streaming
          platform capable of handling trillions of events a day.</td>
        <td style="text-align:left">&#x200B;<a href="https://www.confluent.io/confluent-community-license-faq/">Community License</a> &#x200B;</td>
        <td
        style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://dattell.com/data-architecture-blog/what-is-zookeeper-how-does-it-support-kafka/">Zookeeper</a>&#x200B;</td>
      <td
      style="text-align:left">6.2.0</td>
        <td style="text-align:left">5.4.1</td>
        <td style="text-align:left"><b>ZooKeeper</b> is an <b>open source</b> Apache project that provides a
          centralized service for providing configuration information, naming, synchronization
          and group services over large clusters in distributed systems. When working
          with Apache <b>Kafka</b>, <b>ZooKeeper</b> is primarily used to track the
          status of nodes in the <b>Kafka</b> cluster and maintain a list of <b>Kafka</b> topics
          and messages.</td>
        <td style="text-align:left">&#x200B;</td>
        <td style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://blog.heroku.com/using_netflix_zuul_to_proxy_your_microservices">Zuul</a>&#x200B;</td>
      <td
      style="text-align:left">&#x200B;<a href="https://github.com/Netflix/zuul/tree/v2.3.0">2.3.0</a>&#x200B;</td>
        <td
        style="text-align:left">2.2.2</td>
          <td style="text-align:left"><b>Zuul</b> is an open sourced edge service that proxies requests to multiple
            backing services. It provides a unified &#x201C;front door&#x201D; to your
            system, which allows a browser, mobile app, or other user interface to
            consume services from multiple hosts without managing cross-origin resource
            sharing (CORS) and authentication for each one.</td>
          <td style="text-align:left">&#x200B;<a href="https://www.apache.org/licenses/LICENSE-2.0">Apache <b>License</b> 2.0</a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://www.elastic.co/what-is/elasticsearch">Elasticsearch</a>&#x200B;</td>
      <td
      style="text-align:left">&#x200B;<a href="https://github.com/elastic/elasticsearch/releases/tag/v8.0.0-alpha1">8.0.0</a>&#x200B;</td>
        <td
        style="text-align:left">6.6.2</td>
          <td style="text-align:left"><em><b>Elasticsearch</b></em> is a distributed, free and open search and
            analytics engine for all types of data, including textual, numerical, geospatial,
            structured and unstructured.</td>
          <td style="text-align:left">&#x200B;<a href="https://github.com/elastic/kibana/tree/7.13/licenses/ELASTIC-LICENSE-2.0.txt">Elastic License 2.0</a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://www.elastic.co/what-is/kibana">Kibana</a>&#x200B;</td>
      <td
      style="text-align:left">&#x200B;<a href="https://github.com/elastic/kibana/tree/v8.0.0-alpha1">8.0.0</a>&#x200B;</td>
        <td
        style="text-align:left">6.6.2</td>
          <td style="text-align:left"><em><b>Kibana</b></em> is a free and open frontend application that sits
            on top of the Elastic Stack, providing search and data visualization capabilities
            for data indexed in Elasticsearch.</td>
          <td style="text-align:left">&#x200B;<a href="https://github.com/elastic/kibana/tree/7.13/licenses/ELASTIC-LICENSE-2.0.txt">Elastic License 2.0</a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://fluentbit.io/">fluentbit</a>&#x200B;</td>
      <td
      style="text-align:left">&#x200B;<a href="https://github.com/fluent/fluent-bit/tree/v1.8.3">1.8.3</a>&#x200B;</td>
        <td
        style="text-align:left">1.0.6</td>
          <td style="text-align:left"><em><b>Fluent Bit</b></em> is an open source and multi-platform Log Processor
            and Forwarder which allows you to collect data/logs from different sources,
            unify and send them to multiple destinations. It&apos;s fully compatible
            with Docker and Kubernetes environments.</td>
          <td style="text-align:left">&#x200B;<a href="https://www.apache.org/licenses/LICENSE-2.0">Apache <b>License</b> 2.</a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://www.postgresql.org/">Postgresql</a>&#x200B;</td>
      <td
      style="text-align:left">13.4</td>
        <td style="text-align:left">9.6 and 10.6</td>
        <td style="text-align:left"><em><b>PostgreSQL</b></em> is a powerful, open source object-relational
          database system with over 30 years of active development that has earned
          it a strong reputation for reliability, feature robustness, and performance</td>
        <td
        style="text-align:left">&#x200B;<a href="https://www.postgresql.org/about/licence/">PostGres License</a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://redis.io/">redis</a>&#x200B;</td>
      <td style="text-align:left">&#x200B;<a href="https://github.com/redis/redis/tree/6.2.5">6.2.5</a>&#x200B;</td>
      <td
      style="text-align:left">3.2.6</td>
        <td style="text-align:left"><em><b>Redis</b></em> is an open source (BSD licensed), in-memory data
          structure store, used as a database, cache, and message broker. Redis provides
          data structures such as strings, hashes, lists, sets, sorted sets with
          range queries, bitmaps, hyperloglogs, geospatial indexes, and streams.</td>
        <td
        style="text-align:left">&#x200B;<a href="https://snyk.io/learn/what-is-bsd-license/">BSD License</a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://www.jaegertracing.io/">Jaeger</a>&#x200B;</td>
      <td
      style="text-align:left">&#x200B;<a href="https://github.com/jaegertracing/jaeger/tree/v1.25.0">1.25.0</a>&#x200B;</td>
        <td
        style="text-align:left">1.18</td>
          <td style="text-align:left"><em><b>Jaeger</b></em> is open source software for tracing transactions
            between distributed services. It&apos;s used for monitoring and troubleshooting
            complex microservices environments.</td>
          <td style="text-align:left">&#x200B;<a href="https://www.apache.org/licenses/LICENSE-2.0">Apache <b>Lice</b></a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Dev Stack</b>
      </td>
      <td style="text-align:left"><b>Latest Version</b>
      </td>
      <td style="text-align:left">
        <p><b>&#x200B;</b>
        </p>
        <p><b>&#x200B;</b>
        </p>
        <p><b>Used Version</b>
        </p>
        <p><b>&#x200B;</b>
        </p>
      </td>
      <td style="text-align:left"><b>Description</b>
      </td>
      <td style="text-align:left">
        <p><b>License</b>
        </p>
        <p><b>Type</b>
        </p>
      </td>
      <td style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://openjdk.java.net/">OpenJDK</a>
      </td>
      <td style="text-align:left">JDK11</td>
      <td style="text-align:left">8u212</td>
      <td style="text-align:left"><em><b>OpenJDK</b></em> is completely <b>open source</b> and can be used
        it freely</td>
      <td style="text-align:left">&#x200B;<a href="https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html">GPL-2</a>&#x200B;</td>
      <td
      style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://spring.io/projects/spring-boot">SpringBoot</a>
      </td>
      <td style="text-align:left"> <a href="https://github.com/spring-projects/spring-boot/tree/v2.6.0-M1">2.6.0</a>&#x200B;</td>
      <td
      style="text-align:left">2.2.6</td>
        <td style="text-align:left"><em><b>Spring Boot</b></em> is an open-source micro framework maintained
          by a company called Pivotal. It provides Java developers with a platform
          to get started with an auto configurable production-grade Spring application.</td>
        <td
        style="text-align:left">&#x200B;<a href="https://www.apache.org/licenses/LICENSE-2.0">Apache <b>License</b> 2.0</a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left"><a href="https://reactjs.org/docs/how-to-contribute.html">React</a>
      </td>
      <td style="text-align:left">&#x200B;<a href="https://github.com/facebook/react/tree/v17.0.2">17.0.2</a>&#x200B;</td>
      <td
      style="text-align:left">16.7.0</td>
        <td style="text-align:left"><em><b>React</b></em> is one of Facebook&apos;s first <b>open source</b> projects
          that is both under very active development and is also being used to ship
          code to everybody on facebook.com.</td>
        <td style="text-align:left">&#x200B;<a href="https://www.mit.edu/~amini/LICENSE.md">MIT</a>&#x200B;</td>
        <td
        style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://material-ui.com/">Material-UI-React</a>&#x200B;</td>
      <td
      style="text-align:left">&#x200B;</td>
        <td style="text-align:left">16.8.0</td>
        <td style="text-align:left"><b>Material</b>-<b>UI</b> CE (Community Edition) has been 100% <b>open</b>-<b>source</b> (MIT)
          since the very beginning, and always will be. Developers can ensure <b>Material</b>-<b>UI</b> is
          the right choice for their React applications through <b>Material</b>-<b>UI&apos;s</b> community
          maintenance strategy.</td>
        <td style="text-align:left">&#x200B;<a href="https://www.mit.edu/~amini/LICENSE.md">MIT</a>&#x200B;</td>
        <td
        style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://github.com/nodejs/node">NodeJS</a>&#x200B;</td>
      <td
      style="text-align:left">14.0</td>
        <td style="text-align:left">8.4.0</td>
        <td style="text-align:left">Node. js is an <b>open</b>-<b>source</b>, cross-platform, JavaScript runtime
          environment. It executes JavaScript code outside of a browser.</td>
        <td
        style="text-align:left">&#x200B;<a href="https://www.mit.edu/~amini/LICENSE.md">MIT</a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p><b>DevOps Stack</b>
        </p>
        <p><b>&#x200B;</b>
        </p>
        <p><b>&#x200B;</b>
        </p>
      </td>
      <td style="text-align:left">
        <p><b>&#x200B;</b>
        </p>
        <p><b>Latest Version</b>
        </p>
        <p><b>&#x200B;</b>
        </p>
      </td>
      <td style="text-align:left"><b>Used Version</b>
      </td>
      <td style="text-align:left"><b>Description</b>
      </td>
      <td style="text-align:left"><b>License Type</b>
      </td>
      <td style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">Kubernetes</td>
      <td style="text-align:left">1.22</td>
      <td style="text-align:left">1.18.x</td>
      <td style="text-align:left"><em>Kubernetes</em>, also known as K8s, is an open-source system for automating
        deployment, scaling, and management of containerized applications.</td>
      <td
      style="text-align:left">&#x200B;<a href="https://www.apache.org/licenses/LICENSE-2.0">Apache <b>License</b> 2.0</a>&#x200B;</td>
        <td
        style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">Docker</td>
      <td style="text-align:left">19.03.14</td>
      <td style="text-align:left">19.x</td>
      <td style="text-align:left"><em>Docker</em>, a subset of the Moby project, is a software framework
        for building, running, and managing containers on servers and the cloud.</td>
      <td
      style="text-align:left">&#x200B;<a href="https://www.apache.org/licenses/LICENSE-2.0">Apache <b>License</b> 2.0</a>&#x200B;</td>
        <td
        style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">Helm</td>
      <td style="text-align:left">3.6.3</td>
      <td style="text-align:left">3.x.x</td>
      <td style="text-align:left"><em>Helm</em> helps you manage Kubernetes applications &#x2014; <em>Helm</em> Charts
        help you define, install, and upgrade even the most complex Kubernetes.</td>
      <td
      style="text-align:left">&#x200B;<a href="https://www.apache.org/licenses/LICENSE-2.0">Apache <b>License</b> 2.0</a>&#x200B;</td>
        <td
        style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://www.terraform.io/">Terraform</a>&#x200B;</td>
      <td
      style="text-align:left">1.1.0</td>
        <td style="text-align:left">v0.14.10</td>
        <td style="text-align:left">Terraform allows infrastructure to be expressed as code in a simple, human
          readable language called HCL (HashiCorp Configuration Language).</td>
        <td
        style="text-align:left">&#x200B;<a href="https://github.com/hashicorp/terraform/blob/main/LICENSE">Mozilla Public <em>License</em> 2.0</a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">Jenkins</td>
      <td style="text-align:left">2.306</td>
      <td style="text-align:left">2.289</td>
      <td style="text-align:left"><em>Jenkins</em> &#x2013; an open source automation server which enables
        developers around the world to reliably build, test, and deploy their software.</td>
      <td
      style="text-align:left">&#x200B;<a href="https://www.mit.edu/~amini/LICENSE.md">MIT</a>&#x200B;</td>
        <td
        style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">Go Lang</td>
      <td style="text-align:left">1.16.7</td>
      <td style="text-align:left">1.13.3</td>
      <td style="text-align:left">Go is an open source programming language that makes it easy to build
        simple, reliable, and efficient software.</td>
      <td style="text-align:left">&#x200B;<a href="https://golang.org/LICENSE">3-clause BSD + patent grant</a>&#x200B;</td>
      <td
      style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">Groovy</td>
      <td style="text-align:left">&#x200B;<a href="https://github.com/apache/groovy/releases/tag/GROOVY_3_0_8">3.0.8</a>&#x200B;</td>
      <td
      style="text-align:left">3.0</td>
        <td style="text-align:left">Apache <em>Groovy</em> is a powerful, optionally typed and dynamic language,
          with static-&#x200B;typing and static compilation capabilities, for the
          Java platform aimed at improving developer productivity thanks to a concise, <b>familiar and easy to learn syntax</b>.</td>
        <td
        style="text-align:left">&#x200B;<a href="https://www.apache.org/licenses/LICENSE-2.0">Apache <b>License</b> 2.0</a>&#x200B;</td>
          <td
          style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">Python</td>
      <td style="text-align:left">&#x200B;<a href="https://github.com/python/cpython/releases/tag/v3.9.6">3.9.6</a>&#x200B;</td>
      <td
      style="text-align:left">&#x200B;<a href="https://github.com/python/cpython/releases/tag/v3.9.6">v3.9.6</a>&#x200B;</td>
        <td
        style="text-align:left"><em>Python</em> software and documentation are licensed under the PSF <em>License</em> Agreement.
          Starting with <em>Python</em> 3.8.6,</td>
          <td style="text-align:left">PSF</td>
          <td style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://github.com/mozilla/sops/blob/master/LICENSE">Sops</a>&#x200B;</td>
      <td
      style="text-align:left">&#x200B;<a href="https://github.com/mozilla/sops/releases/tag/v3.7.1">v3.7.1</a>&#x200B;</td>
        <td
        style="text-align:left">&#x200B;<a href="https://github.com/mozilla/sops/releases/tag/v3.7.1">v3.7.1</a>&#x200B;</td>
          <td
          style="text-align:left"><b>sops</b> is an editor of encrypted files that supports YAML, JSON, ENV,
            INI and BINARY formats and encrypts with AWS KMS, GCP KMS, Azure Key Vault,
            age, and PGP.</td>
            <td style="text-align:left">&#x200B;<a href="https://github.com/hashicorp/terraform/blob/main/LICENSE">Mozilla Public <em>License</em> 2.0</a>&#x200B;</td>
            <td
            style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">Ansible</td>
      <td style="text-align:left">&#x200B;<a href="https://github.com/ansible/ansible/releases/tag/v2.11.3">2.11.3</a>&#x200B;</td>
      <td
      style="text-align:left">v2.9.23</td>
        <td style="text-align:left"><em>Ansible</em> is an open source community project sponsored by Red Hat,
          it&apos;s the simplest way to automate IT.</td>
        <td style="text-align:left">GNU General Public <b>License</b>
        </td>
        <td style="text-align:left">&#x200B;</td>
    </tr>
    <tr>
      <td style="text-align:left">&#x200B;<a href="https://blog.stackpath.com/yaml/">yaml</a>&#x200B;</td>
      <td
      style="text-align:left">1.2</td>
        <td style="text-align:left">1.2</td>
        <td style="text-align:left">YAML is a human-readable data serialization standard that can be used
          in conjunction with all programming languages and is often used to write
          configuration files.</td>
        <td style="text-align:left">&#x200B;<a href="https://github.com/yamlcss/yaml/blob/master/License.txt">License</a>&#x200B;</td>
        <td
        style="text-align:left"></td>
    </tr>
  </tbody>
</table>



