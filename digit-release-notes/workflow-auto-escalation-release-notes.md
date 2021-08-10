# Workflow Auto Escalation Release Notes

### Overview <a id="Overview"></a>

This is an enhancement in the workflow service where application can get auto escalated to a designated role on breach of an SLA

### Release Highlights <a id="Release-Highlights"></a>

*  Configure SLA at a workflow state level
* Escalate the application to a role if there is a breach in SLA
* Make the application status as deemed approved or reject on breach of an SLA
* Escalate the application to the next logical step in the workflow ladder if there is a breach in SLA

### Release Features <a id="Release-Features"></a>

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Key Feature</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <ul>
          <li>Configure SLA at a workflow state level</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p>In the earlier version the SLA can be configured only at the business
          service level. Now it has been enhanced in way that either the SLA can
          be configured at a business service level for a business service or it
          can be configured at each workflow state in the business service.</p>
        <p>If Business service has 3 workflow states A-B-C , now there can be SLA
          definition for application movement from A to B and one a separate definition
          for movement from B-C</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <ul>
          <li>Escalate the application to a role if there is a breach in SLA</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p>Either if the SLA breach is at the business service level or at the workflow
          state level ,application can be configured to move the application from
          existing state to a role.</p>
        <p>For Example : If the config is on breach of SLA move the application to
          the Field inspector role , then application will be moved automatically
          to the role field inspector when the SLA timeline is reached.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <ul>
          <li>Make the application status as deemed approved or reject on breach of
            an SLA</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p>On breach of an SLA either at the business service level or at the workflow
          state level , it can be configured to make the application deemed approved
          or rejected.</p>
        <p>Deemed reject will come in use cases where citizen fails to take any action</p>
        <p>Deemed approval will come in use cases where employee fails to take action
          within the stipulated SLA</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <ul>
          <li>Escalate the application to the next logical step in the workflow ladder
            if there is a breach in SLA</li>
        </ul>
      </td>
      <td style="text-align:left">
        <p>On breach of SLA in a workflow state , it can be configured to move the
          application to the next logical state in the workflow ladder.</p>
        <p>For example : if the flow of application is from A-B-C , now in the step
          B if there is a breach in SLA , automatically the application will be moved
          to step C.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Known Issues <a id="Known-Issues"></a>

*  One UX issue which will go out in the next patch release

### Upcoming Release Features <a id="Upcoming-Release-Features"></a>

* 
## Reference Doc Links <a id="Reference-Doc-Links"></a>

| **Doc Links** | **Description** |
| :--- | :--- |
|  |  |
|  |  |

