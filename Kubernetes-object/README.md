# Understanding Kubernetes Objects

Kubernetes Objects are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster. Specifically, they can describe:

- What containerized applications are running (and on which nodes)
- The resources available to those applications
- The policies around how those applications behave, such as restart policies, upgrades, and fault-tolerance

## Object Spec and Status

Every Kubernetes object includes two nested object fields that govern the object’s configuration: ***the object spec*** and ***the object status***. 
- The spec describes your desired state for the object–the characteristics that you want the object to have.
- The status describes the actual state of the object, and is supplied and updated by the Kubernetes system. 

At any given time, the Kubernetes Control Plane actively manages an object’s actual state to match the desired state you supplied. 

Most often, you provide the information to kubectl in a .yaml file. 

## Required Fields

In the .yaml file for the Kubernetes object you want to create, you’ll need to set values for the following fields:

- apiVersion - Which version of the Kubernetes API you’re using to create this object
- kind - What kind of object you want to create
- metadata - Data that helps uniquely identify the object, including a name string, UID, and optional namespace

You’ll also need to provide the object spec field. The precise format of the object spec is different for every Kubernetes object, and contains nested fields specific to that object. The [Kubernetes API Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.13/) can help you find the spec format for all of the objects you can create using Kubernetes. 