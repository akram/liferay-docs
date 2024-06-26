---
header-id: liferay-clustering
---

# @product@ Clustering

[TOC levels=1-4]

<aside class="alert alert-info">
  <span class="wysiwyg-color-blue120">This document has been updated and ported to <a href="https://learn.liferay.com/dxp/latest/en/installation-and-upgrades/setting-up-liferay/clustering-for-high-availability.html">Liferay Learn</a> and is no longer maintained here.</span>
</aside>

@product@ can serve everything from the smallest to the largest web sites. Out
of the box, it's configured optimally for a single server environment. If one
server isn't sufficient to serve your site's high traffic needs, @product@
scales to the size you need. 

![Figure 1: @product@ is designed to scale to as large an installation as you need.](../../../images/clustering-enterprise-configuration.png) 

@product@ works well in clusters of multiple machines (horizontal cluster) or in
clusters of multiple VMs on a single machine (vertical cluster), or any mixture
of the two. Once you have @product@ installed on more than one application
server node, there are several optimizations that must be made. At a minimum,
@product@ should be configured in the following way for a clustered environment:

1.  [All nodes should point to the same database or database  cluster.](/docs/7-2/deploy/-/knowledge_base/d/point-all-nodes-to-the-same-database) 

2.  [Documents and Media repositories must have the same configuration and be accessible to all nodes of the cluster.](/docs/7-2/deploy/-/knowledge_base/d/configure-documents-and-media-the-same-for-all-nodes) 

3.  [Search should be on a separate search server that is optionally clustered.](/docs/7-2/deploy/-/knowledge_base/d/clustering-search) 

4.  [Cluster Link must be enabled so the cache replicates across all nodes of the cluster.](/docs/7-2/deploy/-/knowledge_base/d/enabling-cluster-link) 

5.  [Applications must be auto-deployed to each node individually.](/docs/7-2/deploy/-/knowledge_base/d/auto-deploy-to-all-nodes) 

Many of these configuration changes can be made by adding or modifying
properties in your `portal-ext.properties` file. Remember that this file
overrides the
[defaults](@platform-ref@/7.2-latest/propertiesdoc/portal.properties.html)
in the `portal.properties` file. It's a best practice to copy the relevant
section you want to modify from `portal.properties` into your
`portal-ext.properties` file, and then modify the values there. 

| **Note:** This documentation describes a @product@-specific cluster
| configuration without getting into specific implementations of third party
| software, such as Java EE application servers, HTTP servers, and load
| balancers. Please consult your documentation for those components of your
| cluster to configure those components. Before creating a @product@ cluster,
| make sure your OS is not defining the hostname of your box to the local 
| network at 127.0.0.1. 

Each step defined above is covered below to give you a step by step process for
creating your cluster. Start with making all Nodes point to the same database. 
