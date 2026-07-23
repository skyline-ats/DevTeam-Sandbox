# Objects Overview, Management, and Dynamic Attributes

As you prepare to deploy Cisco Secure Firewall Threat Defense, you realize how much the configuration relies on the use of objects. Organizing reusable objects and dynamic resources from the start simplifies policy management, reduces administrative effort, and makes it easier to adapt as your network and cloud environments evolve.

This training explains how to create and manage objects, object groups, and dynamic attributes to build scalable, reusable, and easier-to-maintain firewall policies.

## Object Fundamentals

Objects are reusable containers that store values referenced throughout Secure Firewall Management Center, including access control policies, NAT rules, event searches, reports, and dashboards.

Objects can be managed from two places in Cisco Secure Firewall Management Center:

- **Object management page:** Where all objects in the system exist; from which they can be added, deleted, or modified.
- **Inline pop-up editor:** Whenever an object is required in specific configuration pages, there is a green + icon that can be used to add an object on demand. However, an object cannot be deleted or modified this way.

The following figure illustrates how to access the object management page by selecting **Objects** from the management center menu on the left:

![alt text here](images/topics/sncf-10-no-001.png)

Secure Firewall Threat Defense supports three types of objects:

- **Host:** A single IP address (for example, 209.165.200.225)
- **Range:** A range of IP addresses (for example, 209.165.200.225–209.165.200.250)
- **Network:** A subnet (for example, 209.165.200.224/27)

Cisco Secure Firewall Management Center includes many predefined objects, and you can create additional objects to match your deployment. Additionally, objects can be added to the management center by importing them from a comma-separated-values (CSV) file.

## Object Groups

Object groups combine multiple objects into a single reusable container, simplifying policy creation and management. Instead of referencing individual objects in a rule, you reference the object group. Changes to the group automatically apply wherever the group is used.

The following figure illustrates how to configure a network group:




<CustomNote>

![Icon](images/shared/theme-case-study.svg)

**Use Case**

You might create an object group named **WLAN_MGMT** that contains all wireless management subnets. Access control rules can then reference the object group instead of individual network objects. As additional wireless management subnets are added, you simply update the object group rather than modifying every policy that uses those networks.

</CustomNote>



Consider the following when using object groups:

- Object and object group names must be unique within their type.
- Deleting a group removes only the group, not the member objects.
- Groups in active policies cannot be deleted.
- Editing an object group used by a policy requires you to re-deploy the policy.

## Dynamic Attributes

Dynamic attributes allow Secure Firewall Threat Defense to automatically update object membership as cloud resources change. Rather than manually maintaining IP addresses, the firewall retrieves current information from the external provider and updates the associated dynamic object.

The following figure illustrates how a new AWS virtual server is automatically added to a dynamic object through Cisco Secure Dynamic Attributes Connector (CSDAC):

![alt text](../images/topics/sncf-10-no-003.PNG)

As shown in the example, instead of creating an Access Control Policy rule:

- **Source:** 10.10.10.0/24
- **Destination:** 192.168.110.0/24, 192.168.111.0/24, 192.168.112.0/24

You can create an Access Control Policy rule:

- **Source:** 10.10.10.0/24
- **Destination:** **AWS-Production-Servers** (a dynamic object populated from an AWS tag).

A dynamic attribute defines how an object is populated, rather than specifying the actual IP addresses. Therefore, as new servers are deployed or removed, the firewall updates the object automatically without requiring a policy change.

<TabsHorizontal>

# Supported Dynamic Attributes

Depending on Secure Firewall Threat Defense software version and licensed integrations, dynamic attributes can include:

- Amazon Web Services (AWS) tags (instances, VPCs, or security groups)
- Azure resource tags
- Cloud metadata
- Secure Dynamic Objects (SDOs) provided by Cisco or external feeds
- Custom external object feeds (depending on deployment)

# Benefits of Dynamic Attributes

- Eliminates manual updates when cloud IP addresses change.
- Simplifies policy management.
- Reduces configuration errors.
- Keeps access control rules synchronized with cloud infrastructure.
- Supports automation and DevOps workflows.

# Dynamic Object Configuration

The two steps of configuring dynamic attributes in Secure Firewall Management Center are:

1. Enable the Cisco Secure Dynamic Attributes Connector (CSDAC) at **Integrations > Dynamic Attributes Connector**.
2. Define the attributes as dynamic objects at **Objects > External Attributes > Dynamic Attributes**.

The following screenshot shows the Dynamic Objects page in Secure Firewall Management Center, where you configure Cisco Secure Dynamic Attributes Connector (CSDAC) integration:

![Insert Alt Text Here](images/topics/sncf-10-no-004.PNG)

# Section Two

Content for section two.

</TabsHorizontal>


### 



Before you can create dynamic objects, you must choose how CSDAC will be deployed and complete the required setup. Depending on your environment, CSDAC can run integrated with the management center, embedded in Security Cloud Control (SCC), or as an on-premises connector. Each option guides you through the prerequisites, such as enabling CSDAC, creating connectors to cloud providers, defining filters to identify the resources to track, and configuring adapters that synchronize the discovered resources with the management center.

Once this initial configuration is complete, you can create dynamic objects whose membership is updated automatically as cloud resources change, eliminating the need to manually maintain IP addresses.

After a dynamic object is created it can then be used anywhere a network object is supported, such as:

- Access Control Policy rules
- NAT rules (where supported)
- Security Intelligence policies (depending on object type)
- Other policy components that accept network objects

<QuestionMC>

Which statement accurately describes how a dynamic attribute object differs from a standard network object in Cisco Secure Firewall Management Center?

::: Answers

- [ ] It stores multiple static IP addresses that must be updated manually after cloud changes.
- [x] It defines how addresses are populated from an external source rather than listing specific IP addresses.
- [ ] It combines multiple existing network objects into a reusable container that policies reference.
- [ ] It creates temporary translations that automatically expire after a configurable timeout.

::: Feedback

Dynamic attribute objects populate their contents from external sources, allowing firewall policies to stay synchronized automatically as cloud resources change.

</QuestionMC>

- first
   - sublist
- second
- third
