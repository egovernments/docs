# FSM Implementation - Configuration

## MDMS Configuration

### FSTP Plant Info

The FSTP plant info contains plant operational capacity per day of each ULB and other plant-related information. It is required to calculate the FSTP capacity utilization in percentage form. MDMS file details:

[egov-mdms-data/FSTPPlantInfo.json at QA · egovernments/egov-mdms-data](https://github.com/egovernments/egov-mdms-data/blob/QA/data/pb/FSM/FSTPPlantInfo.json)\`\`

```
{
	"MdmsCriteria": {
		"tenantId": "pb",
		"moduleDetails": [{
			"moduleName": "dss-dashboard",
			"masterDetails": [{
				"name": "dashboard-config"
			}]
		}, {
			"moduleName": "FSM",
			"masterDetails": [{
				"name": "FSTPPlantInfo"
			}]
		}]
	}
}
```
