---
title: "HIM Configuration Rules"
weight: 1
---
## Configuration Overview

HIM supports structuring information into different trees instead of bundling it all into one tree.
This is likely to lead to that e. g. a server that manages a super domain of somewhat heterogeneous information
will have that information represented by multiple trees.
HIM enables this "forest of trees" to be accessed in a homogeneous manner by using the paths of the nodes of the trees to address theinformation contained in the trees.
To support the server in managing this forest of trees, a HIM configuration tree provides a representation of the key parameters of this forest.
The server may also share this configuration file on request from clients, in order for them to discover the information available by the forest.
The HIM model is not restricted to client/server models.

A file containing this configuration shall have a name starting with "HIM_configuration", 
with an optional suffix that might describe the domain, information type, or version.
The file may have the extension ".him", which typically would indicate that it is YAML formatted.
Any file extension can be used that indicates it has been transformed from its YAML source format to a different format like ".json". 

The configuration tree root node shall have a name starting with "HIM_config", which may be followed by additional information
such as a descriptive domain name, version, etc. 

A server may share the information of this file with a client that wants to discover what information the server manages.

A HIM compliant server shall be able to read a HIM configuration file and from that access the forest of trees it defines.

A HIM compliant tree must follow the HIM rule set.
The project specifying this tree must also define the `domain` metadata for this tree,
and it may provide a `public` URL to a file containing the complete tree,
possible also multiple `public` URLs to renditions of the tree in different formats such as YAML, JSON, etc.

The creation of a HIM configuration file is the responsibility of the HIM server implementor.

## Configuration node types

The following node types can be used in a configuration tree:
1. [Branch](/hierarchical_information_model/common_rule_set/node_types/branch/)
2. [Taxonomy](/hierarchical_information_model/configuration_rule_set/node_types/taxonomy/)
3. [Proxy](/hierarchical_information_model/configuration_rule_set/node_types/proxy/)

## Configuration Tree Example
This example shows a forest consisting of three local trees, and a remote tree:
1. A local tree containing passenger car related signals, having the root node name VehicleData.
2. A local tree containing passenger car related services, having the root node name VehicleServices.
3. A local tree containing type passenger car related ype definitions, having the root node name Types.
4. A remote tree containing charge station related signals, having the root node name ChargingStationData.
- 

```YAML
HIM:
  type: branch
  description: Contains the set of trees that are managed as one virtual domain.


VehicleData:
  type: taxonomy
  domain: Vehicle.Car.ResourceData
  version: X.Y.Z
  local: file://<full-path-name>
  public: https://himrepo.oem.com?taxonomy=Vehicle.Car.ResourceData.X.Y.Z
  description:  ….

VehicleServices:
  type: taxonomy
  domain: Vehicle.Car.ServiceData
  version: X.Y.Z
  local: file://<full-path-name>
  public: https://himrepo.oem.com?taxonomy=Vehicle.Car.ServiceData.X.Y.Z
  description:  ….

Types:
  type: taxonomy
  domain: Vehicle.Car.TypeDefinition
  version: X.Y.Z
  local: file://<full-path-name>
  public: https://himrepo.oem.com?taxonomy=Vehicle.Car.DataType.X.Y.Z
  description:  ….


ChargingStationData:
  type: proxy
  domain:ChargingStation.Vehicle.ResourceData
  version: X.Y.Z
  public: https://himrepo.energyco.com?taxonomy=ChargingStation.Vehicle.ResourceData.X.Y.Z
  description:  ….
  ```
