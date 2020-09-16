# Upgrades and Patches

### Upgrade Instructions

* DIGIT 2.0 is a baselined release - considering simplification and standardization as a theme. It is strongly recommended all-state teams upgrade to leverage benefits.
  * All services versioning will follow [**SemVer 2.0**](https://medium.com/@pmuens/understanding-semver-3f75d11b4d)**,** naming conventions and Git Tagging are improved for better tracing.
  * Next release might have a few more enhancements to the services naming conventions and handling MDMS and Configs better.

### **Upgrade Impact**

Functionally, the upgrade to DIGIT 2.0 should not impact the existing environments.

### List of upgrades

{% tabs %}
{% tab title="Functional Upgrades" %}
<table>
  <thead>
    <tr>
      <th style="text-align:left">Update</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Baseline version upgrades</td>
      <td style="text-align:left">
        <p></p>
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
        <p></p>
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
      <th style="text-align:left">Update</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Enhancements</td>
      <td style="text-align:left">
        <p></p>
        <ul>
          <li>Versioned Git Tags for all the services</li>
          <li>Versioned MDMS and Config data</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>
{% endtab %}
{% endtabs %}

