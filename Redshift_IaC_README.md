# Redhsift IaC (Infrastructure as Code) Utility

Link to Code: [Redshift_IaC_Utility](https://github.com/satyam671/Tune-Pipeline-Music-Streaming-Data-Warehouse/blob/main/Redshift_Cluster_IaC.py)

This utility automates the Infrastructure deployment and configuration for the Redshift cluster along with the prerequisites to spin up the cluster. 

The code performs 3 setups:

 - Create or delete an IAM role and apply appropriate policy to allow access to other AWS services 
 - Create or delete a VPC security group, with appropriate Inbound rules to allow connection to the cluster.
 - Finally, spin up a cluster using the Hardware configurations defined in the config file, set up master DB configs, apply cluster permissions with the IAM role and set VPC security groups as created above.

### Setup Configurations File - cluster.config

    [AWS]
    KEY=<Your Access Key>
    SECRET=<Your Secret Access Key>
    
    [DWH] 
    DWH_CLUSTER_TYPE=<single or multi-node cluster>
    DWH_NUM_NODES=<number of nodes>
    DWH_NODE_TYPE=<Node type e.g. dc2.large>
    DWH_CLUSTER_IDENTIFIER=<cluster identifier>
    DWH_DB=<db name>
    DWH_DB_USER=<db user>
    DWH_DB_PASSWORD=<db password>
    DWH_PORT=<db port. default - 5439>
    
    
    [IAM_ROLE]
    NAME=<role-name>
    DESCRIPTION=<role-description>
    POLICY_ARN=<policy-arn e.g - arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess>
    
    [SECURITY_GROUP]
    NAME=<redshift-security-group-name>
    DESCRIPTION=<security-group-description>
    
    [INBOUND_RULE]
    TYPE=<Redshift>
    PROTOCOL=<protocol e.g - TCP>
    PORT_RANGE=<port>
    CIDRIP=<Specify a single IP address, or an IP address range in CIDR notation>
    DESCRIPTION=<description>

 ### Usage 
 

    > python Redshift_Cluster_IaC.py -h
    
    usage: Redshift_Cluster_IaC.py [-h] -c  -d  [-v]
    
    A Redshift cluster IaC (Infrastructure as Code). It creates an IAM role for the
    Redshift creates a security group and sets up ingress parameters. Finally, spin-
    up a redshift cluster.
    
    required arguments:
      -c, --create      True or False. Create IAM roles, security groups and
                         redshift cluster if it does not exist.
      -d, --delete      True or False. Delete the roles, security group and
                         cluster. WARNING: Deletes the Redshift cluster, IAM role
                         and security group.
    
    optional arguments:
      -v, --verbosity   Increase output verbosity. The default is set to DEBUG. 
    
### How to run
Create a new cluster: 

    python Redshift_Cluster_IaC.py --create TRUE --delete FALSE --verbosity TRUE

Delete cluster:

    python Redshift_Cluster_IaC.py --create FALSE --delete TRUE --verbosity TRUE



</br>
</br>
