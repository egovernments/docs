---
description: 'New release features, enhancements, and fixes'
---

# Release Notes

### Release Summary

DIGIT 2.0 is a baselined release that has got few functional changes, but more of non-functional standardisation changes.

### New ‌Feature Additions <a id="New-&#x200C;Feature-Additions"></a>

{% tabs %}
{% tab title="Functional Release" %}
<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Advance Payments</td>
      <td style="text-align:left">
        <p>Ability to handle <a href="https://digit-discuss.atlassian.net/wiki/spaces/ED/pages/604307457/Release+Notes+for+Advance+Payment+implementation+in+W+S">advanced payments</a> -
          platform and Reference implementation in W&amp;S.</p>
        <p>Advance Collection integration with W&amp;S</p>
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}

{% tab title="Non-Functional Release" %}
<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Infra/Ops Simplification &amp; Enablement</td>
      <td style="text-align:left">
        <p>Infra &amp; Service monitoring v1.0.0 (Prometheus, Alertmanager &amp;
          Grafana)</p>
        <ul>
          <li>Cluster Resource monitoring</li>
          <li>Request Traffic monitoring</li>
          <li>DIGIT Service monitoring</li>
          <li>All Java-based services SpringBoot upgraded from 1.5.X to 2.2.6 for better
            security, performance and metrics.</li>
          <li>Backbone Services migrated to Helm templates to ease deployment on Kubernetes.</li>
          <li>Introduced Minio as a digit platform service for SDCs to leverage S3 like
            object storage feature.</li>
          <li>DIGIT on Spot Instances for AWS users saves 60% of the cloud cost.</li>
          <li>Configurable SSO with GitHub or Google SSO OAuth for all the Infra apps
            like Jaeger, Grafana, Kibana.</li>
          <li><a href="https://github.com/egovernments/CIOps">Jenkins CI/CD as a servic</a>e
            with the pipelines</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}
{% endtabs %}

### Upgrade Instructions <a id="Upgrade-Instructions"></a>

* DIGIT 2.0 is a baselined release - considering simplification and standardization as a theme. It is strongly recommended all-state teams upgrade to leverage benefits.
  * All services versioning will follow [**SemVer 2.0**](https://medium.com/@pmuens/understanding-semver-3f75d11b4d)**,** naming conventions and Git Tagging are improved for better tracing.
  * Next release might have a few more enhancements to the services naming conventions and handling MDMS and Configs better.
* **Impact**: Functionally, the upgrade to DIGIT 2.0 will not impact the existing environments.

{% tabs %}
{% tab title="Functional Upgrades" %}
<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Updated Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Baseline version upgrades</td>
      <td style="text-align:left">
        <ul>
          <li>Bulk persister changes to support bulk persisting for migration in Persister
            Service.</li>
          <li>Localization URL params to be changed to request params in Localization
            service</li>
          <li>Receipt download link in SMS and email notifications.</li>
          <li>Rainwater Harvesting attribute in Property Service</li>
          <li>Filestore service enhancement - Support for SDC and S3 implementation.</li>
          <li>Maven dependencies upgrade and merging the backend services to the master
            branch (Upgraded Tracer to 2.0.0, spring boot to 2.2.6, flyway-core to
            6.4.3, etc along with code cleanup) for all the services across the services.
            The Changelog has been added.</li>
          <li>Baseline versioning of all the services as per the streaming strategy.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">UI Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Generalized Client-side PDF generation component and integration with
            Property, Fire NOC, Trade License, and W&amp;S applications).</li>
          <li>Generalize acknowledgement screens component</li>
          <li>MDMS namespace common component and integration with PT and TL modules.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}

{% tab title="Non-Functional Upgrades" %}
<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Updated Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Enhancements</td>
      <td style="text-align:left">
        <ul>
          <li>Versioned Git Tags for all the services</li>
          <li>Versioned MDMS and Config data.</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}
{% endtabs %}

### Fixes and Enhancements <a id="Fixes-and-Enhancements"></a>

* Upgrading spring boot and tracer version of all the backend services to enhance the range of non-functional benefits like performance, metrics, and security.
* All digit services/configs are baselined to follow the Semantic Versioning. These would enable the partner eco-system, system Integrators and state teams for easy on-going upgrades and integrations.

### ‌Document Resources and Links <a id="&#x200C;Document-Resources-and-Links"></a>

UI Technical Documents

* [PGR](https://digit-discuss.atlassian.net/l/c/U01pjZQ1)
* [Property Tax](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/53542929/Property+Tax+-+UI?atlOrigin=eyJpIjoiNzkwMGY4ZWYyYjJhNDVhOWEzMTg4ZWExNTg0MGU0YjgiLCJwIjoiYyJ9)
* [Trade License](https://digit-discuss.atlassian.net/l/c/57TggeCL)
* [Fire NOC](https://digit-discuss.atlassian.net/l/c/fcwPm0NC)
* [Bill Genie](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/436502610/BillGenie?atlOrigin=eyJpIjoiN2EzZmY2ZjFlYzIxNDc2Zjk4YzIwM2FmOGI1NmM1MDAiLCJwIjoiYyJ9)
* [MCS](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/438894719/Universal+Collection?atlOrigin=eyJpIjoiNjAzNzBiMTAwMzNlNDk2NDk0ZTQxNjdlMzMwYzE5N2IiLCJwIjoiYyJ9)
* [Common Pay](https://digit-discuss.atlassian.net/l/c/NjoYpKzK)
* [Advance Payment](https://digit-discuss.atlassian.net/l/c/i7T9cbxf)
* [mSeva 2.0](https://digit-discuss.atlassian.net/l/c/QX3zRcjW)
* [Water & Sewerage](https://digit-discuss.atlassian.net/l/c/Eg1iS0ba)
* [MDMS UI Configurations](https://digit-discuss.atlassian.net/l/c/AfRS5iZw)
* [Required documents dialogue implementation](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/449085476/Required+documents+dialog+implementation?atlOrigin=eyJpIjoiNDEwZDdkNWYzY2EwNDRkZWE0Nzg2NTcwOTM5NDg1YzMiLCJwIjoiYyJ9)
* [Generation of Acknowledgement PDF](https://digit-discuss.atlassian.net/l/c/dVxJH2B5)
* [How to add dynamic dropdown for MDMS data ](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/450789466/How+to+add+dynamic+drop+down+for+mdms+data?atlOrigin=eyJpIjoiNDY0ZGQxY2RhNTBkNDExOWE4ZTc1MTUxOTk4MTZmOTAiLCJwIjoiYyJ9)
* [Common Acknowledgment screens](https://digit-discuss.atlassian.net/wiki/spaces/EGR/pages/572522501/Acknowledgment+screens?atlOrigin=eyJpIjoiNWI5YzdmZDkyNThmNGI4MGFlMjI2MDg0NzRkMWQ4ZTgiLCJwIjoiYyJ9)

Backend Service Documents

* [Advance Payment](https://digit-discuss.atlassian.net/l/c/1P512Vzx)
* [Kafka Connect for reindex](https://digit-discuss.atlassian.net/l/c/41XVUCh6)
* [TL Service Renewal Upgradation](https://digit-discuss.atlassian.net/l/c/cRAR1xcf)
* [Filestore service](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/37060620/File-Store-Service?atlOrigin=eyJpIjoiOWQwYWZmYjNkNTU0NDFlMzk4YjdiNTk1YTI3ZDY3NTciLCJwIjoiYyJ9)
* [Persister Service](https://digit-discuss.atlassian.net/l/c/hydmp2YA)
* [Collection Migration v1 to v2](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/152567827/Collection+Migration+V1+to+V2?atlOrigin=eyJpIjoiNjEwNjQ1MWE5ZDNmNGU5Nzk0MWI5YWJlNjU0N2E1YWQiLCJwIjoiYyJ9)
* [Consumer Code Uniqueness Migration](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/155910170/Consumer+Code+Uniqueness+Migration?atlOrigin=eyJpIjoiMTc5Y2Q1OWQ0NDBmNDA2MmJhNjRjZGY5NjY3ZTJjYWQiLCJwIjoiYyJ9)
* [Property Registry Migration](https://digit-discuss.atlassian.net/l/c/dgM6oHg1)
* [Notification SMS service](https://digit-discuss.atlassian.net/l/c/0y774J0V)
* [Water Service](https://digit-discuss.atlassian.net/wiki/spaces/EPE/pages/328925216/Water+Service+-+Technical+Document?atlOrigin=eyJpIjoiNDM4Yjc3MmJmNDBiNDViZGEwZjJmYTg2MzVhNDdkOTgiLCJwIjoiYyJ9)
* [Sewerage Service](https://digit-discuss.atlassian.net/l/c/PM2Ho3A1)
* [Water Calculator Service](https://digit-discuss.atlassian.net/l/c/p3MGjvPw)
* [Sewerage Calculator Service](https://digit-discuss.atlassian.net/l/c/o0gRiR1n)
* [W&S Promotion document](https://digit-discuss.atlassian.net/l/c/Z2yYBY2b)

Infra/Deployment Documents

* [Monitoring & Alerting](https://github.com/egovernments/eGov-infraOps/commit/274aab0e90a10673972ddc769f2fc89015f0fe8d)
* [SSO OAuth \(GitHub\)](https://github.com/egovernments/eGov-infraOps/commit/4aae58e8560c726a44c9347795fd9db80aaed6c8) for Kibana, Jaeger, etc
* [Grafana](https://github.com/egovernments/eGov-infraOps/commit/c7a4c3d5eb8b188e5083f3e0f33a9405bb995895) dashboard for Infra and Service monitoring
* [Jenkins as a service](https://github.com/egovernments/eGov-infraOps/commit/274aab0e90a10673972ddc769f2fc89015f0fe8d) for CI/CD
* Minio [Helm templates](https://github.com/egovernments/eGov-infraOps/pull/764/files)



