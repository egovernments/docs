# Configuration Changes

### **MDMS changes**

| **Feature** | **Status** | **Changes** | **Description** |
| :--- | :--- | :--- | :--- |
| BPA | New | [PR-1123](https://github.com/egovernments/egov-mdms-data/pull/1123/files) | To add order for the documents |
| BPA | Deprecate | [PR-1037](https://github.com/egovernments/egov-mdms-data/pull/1037/files) | removed the sanction for OC low application |
| BPA | Update | [PR-1118](https://github.com/egovernments/egov-mdms-data/pull/1118/files) | To update disclaimer |
| BPA | Update | [PR-1062](https://github.com/egovernments/egov-mdms-data/pull/1062/files) | Changed url - bpa to land |
| BPA | New | [PR-1019](https://github.com/egovernments/egov-mdms-data/pull/1019/files) | Added idFormat for OC |
| BPA | New | [PR-1016](https://github.com/egovernments/egov-mdms-data/pull/1016/files) | Added checklist for OC |
| BPA | Update | [PR-1008](https://github.com/egovernments/egov-mdms-data/pull/1008/files) | Updated usages |
| BPA | Update | [PR-1007](https://github.com/egovernments/egov-mdms-data/pull/1007/files) | Updated Sub occupancy type |
| BPA | Update | [PR-1006](https://github.com/egovernments/egov-mdms-data/pull/1006) | Updated Occupancy type |
| BPA | New | [PR-997](https://github.com/egovernments/egov-mdms-data/pull/997) | Added tax period for OC |
| BPA | New | [PR-996](https://github.com/egovernments/egov-mdms-data/pull/996/files) | Added taxheadmaster for OC |
| BPA | New | [PR-995](https://github.com/egovernments/egov-mdms-data/pull/995/files) | Added billing service for OC |
| BPA | Update | [PR-1162](https://github.com/egovernments/egov-mdms-data/pull/1162/files) | Changed id format for bpa permit |
| W&S | Update | [PR-1043](https://github.com/egovernments/egov-mdms-data/pull/1043) | To update the ID format |
| W&S | Update | [PR-1058](https://github.com/egovernments/egov-mdms-data/pull/1058) | to update application types |
| TL | Update | [PR-1160](https://github.com/egovernments/egov-mdms-data/pull/1160) | Updated URL for Required doc screen |
| TL | Update | [PR-1125](https://github.com/egovernments/egov-mdms-data/pull/1125) | Updated rebate and penalty |
| TL | Update | [PR-1133](https://github.com/egovernments/egov-mdms-data/pull/1133) | TL Renewal changes |
| UC | New | [PR-1106](https://github.com/egovernments/egov-mdms-data/pull/1106) | Added disclaimer in the footer |
| Localization | New | [PR-1073](https://github.com/egovernments/egov-mdms-data/pull/1073) | Added new action for v2 localisation search |
| Reports | Deprecate | [PR-1170](https://github.com/egovernments/egov-mdms-data/pull/1170) | Disabling the Reports and UI localization Links |

### Backend Config Changes

| **Module** | **Action** | **PR** | **Description** |
| :--- | :--- | :--- | :--- |
| W&S | Update | [PR-357](https://github.com/egovernments/configs/pull/357) | To update bill PDF advance adjusted changes |
| W&S | Update | [PR-340](https://github.com/egovernments/configs/pull/340) | To Update PDF format |
| W&S | Update | [PR-342](https://github.com/egovernments/configs/pull/342) | To add Advance and pending amount conditional logic |
| W&S | Update | [water-meter.yml](https://github.com/egovernments/configs/commit/d213b8fbc71c8adc67df393b30c8be9ea923e24f#diff-cad1acac07cf6e6c1843536937285a4d) | To add tenant Id in the eg\_ws\_meterreading table |
| W&S | Update | [ws-bill.json](https://github.com/egovernments/configs/commit/900e8e1c59ebc12f4bea49f52063f524aabf3830#diff-b5d08abcd9524da252a33fcff4c515f8) | To update the WS bill PDF format |
| BillGenie | Update | [bill-genie.yml](https://github.com/egovernments/configs/commit/0f3708cdcf6fba00aa36aab5baeae9a7eeb3ab62#diff-9352898a62515ccb3822f24506a37090) | To Update lower cases search |
| BPA | Update | [land-persister.yml](https://github.com/egovernments/configs/commit/5682f1adb60b40663fe13d545e0c865ad4537b08) | Added audit details for owner |
| BPA | Deprecate | [bpa-persister.yml](https://github.com/egovernments/configs/commit/9ae764474a702249cd3aaefa806a3331a37e0364) | Removed land info from bpa-persister |
| BPA | New | [egov-bpa-indexer.yml](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added indexer for bpa |
| BPA | New | [rainmaker-bpastakeholder-indexer.yml](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added indexer for stakeholder Registration |
| BPA | Update | [bpa-revocation.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Changed owners to landinfo and added revocation letter conten |
| BPA | New | [buildingpermit-low.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added report run date |
| BPA | New | [buildingpermit.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added report run date |
| BPA | New | [occupancy-certificate.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added oc certificate |
| BPA | Update | [bpa-revocation.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Updated texts |
| BPA | Update | [buildingpermit.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Changed alignment and added QA code |
| BPA | New | [occupancy-certificate.json](https://github.com/egovernments/configs/commit/47528052b4904ce5ab679324f13165458a83d05a) | Added for OC |
| BPA | Update | [buildingpermit-low.json](https://github.com/egovernments/configs/commit/3da5fcefeedda4b13eda3128b42c8e87aea6697a) | Changed alignment and added QA code |
| BPA | New | [occupancy-certificate.json](https://github.com/egovernments/configs/commit/143dda97f86e06544868ec92d5816766ea128e75) | Added for OC |
| BPA | Update | [noc-persister.yml](https://github.com/egovernments/configs/commit/b94803a5d2e700b56c35b89b8cde5e1e32cfdbc4) | Changed filestore to filestoreId |
| BPA | Update | [noc-persister.yml](https://github.com/egovernments/configs/commit/5f7eafdf3339d49a736d31c50037333a11c0f114) | Updated noc persister |

### Infra Changes <a id="Infra-Change:"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left">Module</th>
      <th style="text-align:left">File Name</th>
      <th style="text-align:left">Action</th>
      <th style="text-align:left">Code Change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">W&amp;S</td>
      <td style="text-align:left">
        <p></p>
        <p>helm/charts/municipal-services/sw-services/values.yaml</p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p>Removed the following details from values.yml</p>
      </td>
      <td style="text-align:left"><code>scid-format: &quot;SW/[CITY.CODE]/[fy:yyyy-yy]/[SEQ_EGOV_COMMON]&quot;</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p></p>
        <p>EGOV_IDGEN_SCID_FORMAT</p>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><code>value: {{ index .Values &quot;scid-format&quot; | quote }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">helm/charts/municipal-services/ws-services/values.yaml</td>
      <td style="text-align:left">Removed the following details from values.yml</td>
      <td style="text-align:left"><code>wcid-format: &quot;WS/[CITY.CODE]/[fy:yyyy-yy]/[SEQ_EGOV_COMMON]&quot;</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">EGOV_IDGEN_WCID_FORMAT</td>
      <td style="text-align:left"></td>
      <td style="text-align:left"><code>value: {{ index .Values &quot;wcid-format&quot; | quote }}</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p></p>
        <p>helm/environments/&lt;env&gt;.yaml</p>
      </td>
      <td style="text-align:left">Autocreate-new-seq flag must be enabled in IdGen Service of environment
        file</td>
      <td style="text-align:left"><code>autocreate-new-seq: &quot;true&quot;</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p></p>
        <p>helm/environments/qa.yaml</p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p>change the key from allowed-file-formats: to <b>allowed-file-formats-map</b>
        </p>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left">
        <p></p>
        <p>helm/charts/municipal-services/firenoc-services/values.yaml</p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p>Added EGOV_DEFAULT_STATE_ID in fire noc environment file to pick up proper
          tenant during search call</p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p></p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">SMS Notification Service</td>
      <td style="text-align:left">helm/charts/core-services/egov-notification-sms/values.yaml</td>
      <td style="text-align:left">
        <p>Added sms.config.map property for SMS changes-Remove the sms.config.map
          from the values.yml file</p>
        <p>It should move to <b>helm/environments/qa.yaml</b>
        </p>
      </td>
      <td style="text-align:left"><code>sms-config-map: &quot;{&apos;User&apos;:&apos;$username&apos;, &apos;passwd&apos;: &apos;$password&apos;, &apos;sid&apos;:&apos;$senderid&apos;, &apos;mobilenumber&apos;:&apos;$mobileno&apos;, &apos;message&apos;:&apos;$message&apos;, &apos;mtype&apos;:&apos;N&apos;, &apos;DR&apos;:&apos;N&apos;, &apos;smsservicetype&apos;:&apos;singlemsg&apos;}&quot;</code>
      </td>
    </tr>
  </tbody>
</table>

### Service Build Artefacts





