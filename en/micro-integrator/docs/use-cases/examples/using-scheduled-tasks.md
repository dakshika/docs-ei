# Using Scheduled Tasks

The sections below demonstrate an example of scheduling a task using the default
implementation, to inject an XML message and to print it in the logs of
the server.

### Creating the Sequence

1.  In the **Project Explorer** , right click the
    **ScheduleDefaultTask** project, and click **New** → **Sequence**
    .  
    ![](attachments/119130430/119130439.png){width="500" height="502"}
2.  Click **Create New Sequence** and click **Next** .
3.  Enter the **InjectXMLSequence** as the sequence name and click
    **Finish** .  
    ![](attachments/119130430/119130438.png){width="500" height="497"}  
4.  Drag and drop a **Log** mediator and a **Drop** mediator from the
    **Mediators** Palette.  
    ![](attachments/119130430/119130437.png){width="550"}  
5.  Click on the **Log** mediator, and in the Properties section enter
    the following details.  
    -   **Log Category:** `            INFO           `
    -   **Log Level:** `            CUSTOM           `

    ![](images/icons/grey_arrow_down.png){.expand-control-image}
    Configuration of the Sequence

    The below is the complete source configuration of the Sequence
    (i.e., the `             InjectXMLSequence.xml            ` file).

    ``` xml
        <?xml version="1.0" encoding="UTF-8"?>
        <sequence name="ScheduleCustomSequence" trace="disable" xmlns="http://ws.apache.org/ns/synapse">
            <log level="custom" />
            <drop />
        </sequence>
    ```
### Create the Scheduled Task

The below is the complete source configuration of the Scheduled Task
    (i.e., the `             InjectXMLTask.xml            ` file).

    ``` xml
        <?xml version="1.0" encoding="UTF-8"?>
        <task class="com.example.post.scheduleTask1.ESBTask" group="synapse.simple.quartz" name="PrintParameterTask" xmlns="http://ws.apache.org/ns/synapse">
            <trigger interval="5" />
            <property name="parameter" value="<abc>This is a scheduled task of the default implementation.</abc>" xmlns:task="http://www.wso2.org/products/wso2commons/tasks"/>
        </task>
    ```

-   **Task Name:** `InjectXMLTask`
-   **Count:** `-1`
-   **Interval (in seconds):** 5

In the **Form View** of the `          InjectXMLTask.xml         `
    file, click the **Task Implementation Properties** button.  
    ![](attachments/119130430/119130433.png){width="650" height="281"}

Select **XML** as the **Parameter Type** of the **message**
    parameter, enter
    `           <abc>This is a scheduled task of the default implementation.</abc>          `
    as the XML message in the **Value/Expression** field and click
    **OK** .  
    ![](attachments/119130430/119130451.png)

### Injecting messages to RESTful Endpoints

In order to use the Message Injector to inject a message to a RESTful endpint, we can specify the injector with the required payload and inject the message to sequence or proxy service as defined above. The sample below shows a RESTful message injection through a ProxyService.

``` java tab='Task Configuration'
<task name="SampleInjectToProxyTask"
                     class="org.apache.synapse.startup.tasks.MessageInjector"
                     group="synapse.simple.quartz">
                  <trigger count="2" interval="5"/>
                  <property xmlns:task="http://www.wso2.org/products/wso2commons/tasks"
                            name="injectTo"
                            value="proxy"/>
                  <property xmlns:task="http://www.wso2.org/products/wso2commons/tasks" name="message">
                     <request xmlns="">
                        <location>
                           <city>London</city>
                           <country>UK</country>
                        </location>
                     </request>
                  </property>
                  <property xmlns:task="http://www.wso2.org/products/wso2commons/tasks"
                            name="proxyName"
                            value="SampleProxy"/>
</task>
```
        
``` java tab='Proxy Configuration'
<proxy name="SampleProxy"
                      transports="https http"
                      startOnLoad="true"
                      trace="disable">
                  <description/>
                  <target>
                     <inSequence>
                        <property name="uri.var.city" expression="//request/location/city"/>
                        <property name="uri.var.cc" expression="//request/location/country"/>
                        <log>
                           <property name="Which city?" expression="get-property('uri.var.city')"/>
                           <property name="Which country?" expression="get-property('uri.var.cc')"/>
                        </log>
                        <send>
                           <endpoint name="EP">
                              <http method="get"
                                    uri-template="http://api.openweathermap.org/data/2.5/weather?q={uri.var.city},{uri.var.cc}"/>
                           </endpoint>
                        </send>
                     </inSequence>
                     <outSequence>
                        <log level="full"/>
                        <drop/>
                     </outSequence>
                  </target>
</proxy>
```

### Viewing the output

You view the XML message you injected (i.e.,
`         <abc>This is a scheduled task of the default implementation.</abc>        `
) getting printed in the logs of the ESB Profile every 5 seconds.

![](attachments/119130430/119130443.png)