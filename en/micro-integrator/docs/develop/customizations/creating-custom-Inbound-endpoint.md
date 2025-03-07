# Creating a Custom Inbound Endpoint

WSO2 Micro Integrator supports several inbound endpoints. However, there can be scenarios that require functionality not provided by the existing inbound endpoints. For example, you might need an inbound endpoint to connect to a certain back-end server or vendor specific protocol.

To support such scenarios, you can write your own custom inbound endpoint by extending the behavior for **Listening**, **Polling**, and **Event-Based** inbound endpoints.

## Instructions

### Step 1: Developing a Custom Inbound Endpoint

- To create a **custom listening inbound endpoint**, download the maven artifact used in the [sample custom listening inbound endpoint configuration](https://github.com/wso2-docs/ESB/tree/master/ESB-Artifacts/inbound/custom_inbound_listening) configuration.

- To create a **custom polling inbound endpoint**, download the maven artifact used in the [sample custom polling inbound endpoint configuration](https://github.com/wso2-docs/ESB/tree/master/ESB-Artifacts/inbound/custom_inbound).

- To create a **custom event-based inbound endpoint**, download the maven artifact used in the [sample custom event-based inbound endpoint configuration](https://github.com/wso2-docs/ESB/tree/master/ESB-Artifacts/inbound/custom_inbound_waiting).

### Step 2: Deploying the Custom Inbound Endpint

You need to copy the built jar file to the `MI_HOME/lib` directory and restart the Micro Integrator to load the class.

### Step 3: Create the Custom Inbound Endpoint

1. If you have already created an [ESB Config project](../../creating-projects/#esb-config-project), right-click the project and go to **New → Inbound Endpoint** to open the **New Inbound Endpoint Artifact**.
2. Select **Create a New Inbound Endpoint** and click **Next**.
3. Type a unique name for the inbound endpoint, and then select **Custom** as the inbound endpoint type.
3. Enter a unique name for the inbound endpoint, and select an **Inbound Endpoint Creation Type** from the list.       
5. Specify the location where the artifact should be saved: Select an existing ESB Config project in your workspace, or click **Create new Project** and create a new project.
5.  Click **Finish**. The inbound endpoint is created in the `src/main/synapse-config/inbound-endpoint` folder under the ESB Config project you specified.
6.  Open the new artifact from the project explorer, go to the **Source View**, and update the following properties:
	<table>
   <thead>
      <tr>
         <th>
            <p>Property Name</p>
         </th>
         <th>
            <p>Description</p>
         </th>
      </tr>
   </thead>
   <tbody>
      <tr>
         <td>
          class
         </td>
         <td>
          Name of the custom class you implementation in <a href="#step-1-developing-a-custom-inbound-endpoint">step 1</a>.
         </td>
      </tr>
      <tr>
         <td>
          sequence
         </td>
         <td>Name of the sequence message that should be injected. Specify a valid sequence name.</td>
      </tr>
      <tr>
         <td>
            onError
         </td>
         <td>Name of the fault sequence that should be invoked in case of failure. Specify a valid sequence name.</td>
      </tr>
      <tr>
         <td>
          inbound.behavior
         </td>
         <td>
          Specify whether your custom endpoint is <code>listening</code>, <code>polling</code>, or <code>event-based</code>.
         </td>
      </tr>
   </tbody>
</table>

## Examples
..

## Guides
..