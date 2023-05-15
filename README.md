# spaceone-initializer

`spaceone-initializer` helps configure spaceone in various modes.

## Default Mode (with Marketplace)

Default mode is configured in the following way.

* Create a root domain to manage the SpaceONE cluster
* Create a user domain for general users.
* Register Open Source Marketplace (grpc://repository.portal.spaceone.dev:50051)

### Values Examples (values.yaml)

~~~
main:
  import:
    - /root/spacectl/apply/root_domain.yaml
    - /root/spacectl/apply/register_marketplace.yaml
    - /root/spacectl/apply/user_domain.yaml
    - /root/spacectl/apply/create_role.yaml
    - /root/spacectl/apply/add_statistics_schedule.yaml
    - /root/spacectl/apply/print_api_key.yaml
  var:
    domain:
      root: root
      user: spaceone
    default_language: ko
    default_timezone: Asia/Seoul
    domain_owner:
      id: admin
      password: Admin123!@#         # Change your password
    user:
      id: system_api_key
    marketplace_endpoint: grpc://repository.portal.spaceone.dev:50051
~~~

### Run the spaceone-initializer with the following command 
~~~
helm install cloudforet-initializer cloudforet/spaceone-initializer -f values.yaml
~~~

## Local Mode (without Marketplace)

Local mode is a configuration for an on-premise environment that cannot connect to the Internet.

* Create a root domain to manage the SpaceONE cluster
* Create a user domain for general users.
* Create a local repository
* Create 4 managed policies

### Values Examples (values.yaml)
~~~
main:
  import:
    - /root/spacectl/apply/root_domain.yaml
    - /root/spacectl/apply/create_local_repository.yaml
    - /root/spacectl/apply/user_domain.yaml
    - /root/spacectl/apply/create_policy.yaml
    - /root/spacectl/apply/create_role.yaml
    - /root/spacectl/apply/add_statistics_schedule.yaml
    - /root/spacectl/apply/print_api_key.yaml
  var:
    domain:
      root: root
      user: spaceone
    default_language: ko
    default_timezone: Asia/Seoul
    domain_owner:
      id: admin
      password: Admin123!@#         # Change your password
    user:
      id: system_api_key
~~~

### Run the spaceone-initializer with the following command
~~~
helm install cloudforet-initializer cloudforet/spaceone-initializer -f values.yaml
~~~

