# spaceone-initializer

SpaceONE initializer

## Root Domain

Root domain is a system domain for over-all user-domain.

* providing plugin service
* providing market-place service

### Create vaules.yaml

~~~
enabled: true
image:
    name: spaceone/spacectl
    version: 1.9.7
main:
  import:
    - /root/spacectl/apply/root_domain.yaml
    - /root/spacectl/apply/marketplace.yaml
    - /root/spacectl/apply/role.yaml
  var:
    domain:
      root: root
    default_language: ko
    default_timezone: Asia/Seoul
    domain_owner:
      id: admin
      password: Admin123!@#
    user:
      id: root_api_key
    consul_server: spaceone-consul-server
    marketplace_endpoint: grpc://repository.portal.spaceone.dev:50051
    project_admin_policy_type: MANAGED
    project_admin_policy_id: policy-managed-project-admin
    project_viewer_policy_type: MANAGED
    project_viewer_policy_id: policy-managed-project-viewer
    domain_admin_policy_type: MANAGED
    domain_admin_policy_id: policy-managed-domain-admin
    domain_viewer_policy_type: MANAGED
    domain_viewer_policy_id: policy-managed-domain-viewer

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
    version: 1.9.7
main:
  import:
    - /root/spacectl/apply/user_domain.yaml
    - /root/spacectl/apply/statistics.yaml
  var:
    domain:
      user: spaceone
    default_language: ko
    default_timezone: Asia/Seoul
    domain_owner:
      id: admin
      password: Admin123!@#
    consul_server: spaceone-consul-server
    marketplace_endpoint: grpc://repository.portal.spaceone.dev:50051
    project_admin_policy_type: MANAGED
    project_admin_policy_id: policy-managed-project-admin
    project_viewer_policy_type: MANAGED
    project_viewer_policy_id: policy-managed-project-viewer
    domain_admin_policy_type: MANAGED
    domain_admin_policy_id: policy-managed-domain-admin
    domain_viewer_policy_type: MANAGED
    domain_viewer_policy_id: policy-managed-domain-viewer

  tasks: []
~~~

### Install spaceone-initializer helm chart
- first, uninstall root-domain if it is installed
    - if you installed spaceone with minikube.yaml, delete initialize-spaceone pod
~~~
helm uninstall root-domain
~~~
- then, install user-domain helm chart
~~~
helm install user-domain -f values.yaml spaceone/spaceone-initializer
~~~

## Root & User Domain
### Create vaules.yaml

~~~
enabled: true
image:
    name: spaceone/spacectl
    version: 1.9.7
main:
  import:
    - /root/spacectl/apply/root_domain.yaml 
    - /root/spacectl/apply/marketplace.yaml
    - /root/spacectl/apply/role.yaml
    - /root/spacectl/apply/user_domain.yaml
    - /root/spacectl/apply/statistics.yaml
  var:
    domain:
      root: root
      user: spaceone
    default_language: ko
    default_timezone: Asia/Seoul
    domain_owner:
      id: admin
      password: Admin123!@#
    user:
      id: root_api_key
    consul_server: spaceone-consul-server
    marketplace_endpoint: grpc://repository.portal.spaceone.dev:50051
    project_admin_policy_type: MANAGED
    project_admin_policy_id: policy-managed-project-admin
    project_viewer_policy_type: MANAGED
    project_viewer_policy_id: policy-managed-project-viewer
    domain_admin_policy_type: MANAGED
    domain_admin_policy_id: policy-managed-domain-admin
    domain_viewer_policy_type: MANAGED
    domain_viewer_policy_id: policy-managed-domain-viewer

  tasks: []
~~~

### Install spaceone-initializer helm chart
~~~
helm install domain -f values.yaml spaceone/spaceone-initializer
~~~
