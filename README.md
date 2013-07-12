# AppDynamics ServiceNow Monitoring Extension

- [Use Case](servicenow-readme.md#use-case)
- [Installation](servicenow-readme.md#installation)
- [Prerequisite](servicenow-readme.md#prerequisite)
- [Contributing](servicenow-readme.md#contributing)

##Use Case
ServiceNow ([http://www.servicenow.com](www.servicenow.com)) is a software-as-a-service (SaaS) provider of IT service management (ITSM) software.
AppDynamics integrates directly with ServiceNow to create tickets in response to alerts. With the ServiceNow integration you can leverage 
your existing ticketing infrastructure to notify your operations team to resolve performance degradation issues.

##Prerequisite
Before you begin integrating your ServiceNow client with AppDynamics, the JSON plugin for ServiceNow must be activated. 

######Activate the JSON plugin in ServiceNow:  
1. In System Definition > Plugins, search for "JSON Web Service".
2. Right-click "JSON Web Service" and click "Activate/Upgrade".

##Installation
1. Modify the paremeters in the IntegrationsSDK/CustomNotification/ticketing/createServiceNowTicket/params.sh file as follows:

	a. Assign the ASSIGN\_TO variable to be a person or department account that is authorized in the ServiceNow system and to which auto generated tickets can be assigned.

	b. Assign the DOMAIN variable to be your ServiceNow domain. For example,

		(DOMAIN="[https://sampledomain.service-now.com](https://sampledomain.service-now.com/)")

	c. Assign the USER variable to be the username that will issue these generated tickets.

	d. Assign the PASSWORD variable to be the password of the entered username that will issue these generated tickets.

2. Modify the createServiceNowTicket.sh file using the following table to correspond with the parameters in the params.sh file:

	<table>
	<tr>
	<td><strong>AppDynamics Parameters</strong></td>
	<td><strong>ServiceNow Parameters</td>
	<td><strong>Comments</td>
	</tr>

	<tr>
	<td> </td>
	<td>assigned_to</td>
	<td>This is the field used to assign an incident to an individual/department. The email address or full name of the designated user can be written here. This should be entered into the params.sh file as an email address that is already configured in the ServiceNow environment.</td>
	</tr>
	
	<tr>
	<td>
	<table>
	
	<tr>
	<td>
	APP_NAME</td>
	</tr>
	
	<tr>
	<td>PVN_ALERT_TIME</td>
	</tr>
	
	<tr>
	<td>SEVERITY</td>
	</tr>
	
	<tr>
	<td>POLICY_NAME</td>
	</tr>
	
	<tr>
	<td>AFFECTED_ENTITY_TYPE</td>
	</tr>
	
	<tr>
	<td>AFFECTED_ENTITY_NAME</td>
	</tr>
	
	<tr>
	<td>EVALUATION_TYPE</td>
	</tr>
	
	<tr>
	<td>EVALUATION_ENTITY_NAME</td>
	</tr>
	
	<tr>
	<td>SCOPE_TYPE_x</td>
	</tr>
	
	<tr>
	<td>SCOPE_NAME_x</td>
	</tr>
	
	<tr>
	<td>CONDITION_NAME_x</td>
	</tr>
	
	<tr>
	<td>THRESHOLD_VALUE_x</td>
	</tr>
	
	<tr>
	<td>  
	 OPERATOR_x</td>
	</tr>
	
	<tr>
	<td>BASELINE_NAME_x</td>
	</tr>
	
	<tr>
	<td>USE_DEFAULT_BASELINE_x</td>
	</tr>
	
	<tr>
	<td>OBSERVED_VALUE_x</td>
	</tr>
	
	<tr>
	<td>INCIDENT_ID</td>
	</tr>
	
	<tr>
	<td>DEEP_LINK_URL</td>
	</tr>
	</table>
	</td>
	<td>description</td>
	<td>The format is as follows for the following Policy Violation Parameters:
	
	<table>
	
	<tr>
	<td><strong>Variable name: Variable value</strong></td>
	</tr>
	
	<tr>
	<td>Application Name: APP_NAME</td></td>
	</tr>
	
	<tr>
	<td>Policy Violation Alert Time: PVN_ALERT_TIME</td>
	</tr>
	
	<tr>
	<td>Severity: SEVERITY</td></td>
	</tr>
	
	<tr>
	<td>Name of Violated Policy: POLICY_NAME</td>
	</tr>
	
	<tr>
	<td>Affected Entity Type: AFFECTED_ENTITY_TYPE</td>
	</tr>
	
	<tr>
	<td>Name of Affected Entity: AFFECTED_ENTITY_NAME</td>
	</tr>
	
	<tr>
	<td>Evaluation Entity #x</td>
	</tr>
	
	<tr>
	<td>Evaluation Entity: EVALUATION_TYPE</td>
	</tr>
	
	<tr>
	<td>Evaluation Entity Name: EVALUATION_ENTITY_NAME</td>
	</tr>
	
	<tr>
	<td>Triggered Condition #x</td>
	</tr>
	
	<tr>
	<td>Scope Type: SCOPE_TYPE_x</td>
	</tr>
	
	<tr>
	<td>
	Scope Name: SCOPE_NAME_x</td>
	</tr>
	
	<tr>
	<td>CONDITION_NAME_x</td>
	</tr>
	
	<tr>
	<td>OPERATOR_x</td>
	</tr>
	
	<tr>
	<td>THRESHOLD_VALUE_x (this is for ABSOLUTE conditions)</td>
	</tr>
	
	<tr>
	<td>Violation Value: OBSERVED_VALUE_x</td>
	</tr>
	
	<tr>
	<td>Incident URL: DEEP_LINK_URL + INCIDENT_ID</td>
	</tr>
	
	</table>
	</td>
	</tr>
	
	<tr>
	<td>SEVERITY</td>
	<td>impact</td>
	<td>Represents the impact of the new Problem. Use the SEVERITY parameter where: ERROR = 1,  WARN = 2, and INFO = 3</td>
	</tr>
	
	<tr>
	<td></td>
	<td>knowledge</td>
	<td>This is either "true" or "false" but for policy violations, leave this as "false".</td>
	</tr>
	
	<tr>
	<td></td>
	<td>known_error</td>
	<td> This is either "true" or "false" but for policy violations, leave this as "true".</td>
	</tr>
	
	<tr>
	<td>PRIORITY</td>
	<td>priority</td>
	<td>This is a value from 1 to 5 where: 1 = Critical, 2 =  High, 3 = Moderate, 4 = Low, 5 = Planning. The PRIORITY parameter will fill this out directly.</td>
	</tr>
	
	</table>

2. Install Custom Actions

	To create a Custom Action using ServiceNow, first refer to the *Installing Custom Actions into the Controller* heading [here](http://docs.appdynamics.com/display/PRO12S/Configure+Custom+Notifications#ConfigureCustomNotifications-InstallingCustomActionsontheController) (requires AppDynamics login.)

	The custom.xml file and createServiceNowTicket directory used for this custom notification are located within the IntegrationsSDK/CustomNotification/ticketing/ directory.

	Place the createServiceNowTicket/ directory (containing params.sh and createServiceNowTicket.sh) along with thecustom.xml file into the \<controller\_install\_dir\>/custom/actions/ directory.

3. Look for the newest created Problem in ServiceNowNow

	When a problem is created through AppDynamics it should look similar to the following screenshots.

	The following is an overview shot of ServiceNow:

![](images/Overview Ticket.png)

The following shows the specifics of the ticket description:

![](images/New Ticket.png)

**Note**: Notice that the "assigned to" field has "Beth Anglin" current in place here. This is simply an example name and if properly inserted into the params.sh file it will display whichever file is needed

  

##Contributing

Always feel free to fork and contribute any changes directly via GitHub.


##Support

For any support questions, please contact ace@appdynamics.com.