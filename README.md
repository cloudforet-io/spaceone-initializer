# spaceone-initializer

SpaceONE initializer

## Root Domain

Root domain is a system domain for over-all user-domain.

* providing pluin service
* providing market-place service

### Create vaules.yaml

~~~
enabled: true
image:
    name: spaceone/spacectl
    version: 1.8.4
domain: root
main:
  import:
    - /root/spacectl/apply/root_domain.yaml 
    - /root/spacectl/apply/marketplace.yaml
    - /root/spacectl/apply/hyperbilling.yaml # If you have a hyperbilling account
  var:
    domain_name: root
    domain_owner:
      id: admin
      password: Adminpassword
    user:
      id: root_api_key
    consul_server: spaceone-consul-server
    marketplace_endpoint: grpc://repository.portal.spaceone.dev:50051
  tasks: []
~~~

### Install spaceone-initializer helm chart
~~~
helm install root-domain -f values.yaml spaceone/spaceone-initializer
~~~

## User Domain

### Create vaules.yaml
~~~
enabled: true
image:
    name: spaceone/spacectl
    version: 1.8.4
domain: user
main:
  import:
    - /root/spacectl/apply/local_domain.yaml
    - /root/spacectl/apply/statistics.yaml

  var:
    domain_name: spaceone
    domain_owner: admin
    domain_owner_password: Admin123!@#
    project_admin_policy_type: MANAGED
    project_admin_policy_id: policy-0386cce2730b
    domain_admin_policy_type: MANAGED
    domain_admin_policy_id: policy-0386cce2730b

  tasks: []
~~~

### Install spaceone-initializer helm chart
- first, uninstall root-domain if it is installed
~~~
helm uninstall root-domain
~~~
- then, install user-domain helm chart
~~~
helm install user-domain -f values.yaml spaceone/spaceone-initializer
~~~