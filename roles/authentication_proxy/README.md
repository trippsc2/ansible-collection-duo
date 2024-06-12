<!-- BEGIN_ANSIBLE_DOCS -->

# Ansible Role: trippsc2.duo.authentication_proxy
Version: 1.0.0

This role installs and configures a DUO Authentication Proxy on a Linux machine.

## Requirements

| Platform | Versions |
| -------- | -------- |
| Debian | <ul><li>bullseye</li><li>bookworm</li></ul> |
| EL | <ul><li>8</li><li>9</li></ul> |
| Ubuntu | <ul><li>focal</li><li>jammy</li><li>noble</li></ul> |

## Dependencies

| Collection |
| ---------- |
| ansible.posix |
| community.general |
| trippsc2.general |

## Role Arguments
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| duoap_configure_selinux | Whether the role will configure SELinux for the DUO Authentication Proxy. | bool | no |  | true |
| duoap_group | The primary group of the `duoap_user` user under which the DUO Authentication Proxy will run. | str | no |  | duo_authproxy_svc |
| duoap_user | The user account as which the DUO Authentication Proxy will run. | str | no |  | duo_authproxy_svc |
| duoap_combine_certs | A list of dictionaries specifying the certificates to combine and the path to which they will be written. | list of dicts of 'duoap_combine_certs' options | no |  |  |
| duoap_base_install_path | The base path where the DUO Authentication Proxy will be installed. The installed version will be placed at `./duoauthproxy-<version>` relative to this path. A symlink will be created at `./duoauthproxy` pointing to the most recently installed version. | path | no |  | /opt |
| duoap_version | The version of the DUO Authentication Proxy to install. If not specified, the latest version will be installed. If another version is already installed and `duoap_upgrade` is set to `false`, the role will not upgrade/downgrade to this version. | str | no |  |  |
| duoap_upgrade | Whether the role will upgrade/downgrade the DUO Authentication Proxy to the specified version, if it is not already installed. | bool | no |  | false |
| duoap_temp_path | The path where temporary files will be stored during the installation process. | path | no |  | /tmp/duoap |
| duoap_cleanup_old_version | Whether the role will remove old versions of the DUO Authentication Proxy after upgrading/downgrading. | bool | no |  | false |
| duoap_log_dir | The directory where DUO Authentication Proxy logs will be stored. | path | no |  | /var/log/duo |
| duoap_configure_logrotate | Whether the role will configure logrotate for the DUO Authentication Proxy. | bool | no |  | true |
| duoap_debug | Whether DUO Authentication Proxy will run in debug mode. | bool | no |  | false |
| duoap_log_auth_events | Whether DUO Authentication Proxy will log authentication events. | bool | no |  | false |
| duoap_log_sso_events | Whether DUO Authentication Proxy will log SSO events. | bool | no |  | false |
| duoap_log_max_files | The maximum number of log files to keep. If `duoap_configure_logrotate` is `true`, this will default to 0. | int | no |  | 6 |
| duoap_log_max_size_in_mb | The maximum size of each log file in megabytes. If `duoap_configure_logrotate` is `true`, this will default to 0. | int | no |  | 10 |
| duoap_http_ca_certs_file | The path to a file containing CA certificates to trust when making HTTP requests. If not specified, the role will use the system default. | path | no |  | OS specific |
| duoap_interface | The network interface on which the DUO Authentication Proxy will listen. | str | no |  |  |
| duoap_http_proxy_host | The hostname of the HTTP proxy server. | str | no |  |  |
| duoap_http_proxy_port | The port of the HTTP proxy server. | int | no |  |  |
| duoap_test_connectivity_on_startup | Whether the DUO Authentication Proxy will test connectivity to the DUO API server on startup. | bool | no |  | false |
| duoap_service_account_username | The username of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory. | str | no |  |  |
| duoap_service_account_password | The password of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory. | str | no |  |  |
| duoap_ikey | The integration key for the DUO Authentication Proxy. | str | no |  |  |
| duoap_skey | The secret key for the DUO Authentication Proxy. | str | no |  |  |
| duoap_api_host | The FQDN of the DUO API server. | str | no |  |  |
| duoap_ad_clients | A list of dictionaries specifying Active Directory clients. | list of dicts of 'duoap_ad_clients' options | no |  |  |
| duoap_radius_clients | A list of dictionaries specifying RADIUS clients. | list of dicts of 'duoap_radius_clients' options | no |  |  |
| duoap_duo_only_client_enabled | Whether the DUO Authentication Proxy will only allow DUO authentication. | bool | no |  | false |
| duoap_ldap_auto_servers | A list of dictionaries specifying LDAP auto servers. | list of dicts of 'duoap_ldap_auto_servers' options | no |  |  |
| duoap_radius_auto_servers | A list of dictionaries specifying RADIUS auto servers. | list of dicts of 'duoap_radius_auto_servers' options | no |  |  |
| duoap_configure_dirsync | Whether the role will configure directory synchronization. | bool | no |  | false |
| duoap_dirsync_ikey | The integration key for directory synchronization. If not specified, the role will use the `duoap_ikey` variable. | str | no |  |  |
| duoap_dirsync_skey | The secret key for directory synchronization. If not specified, the role will use the `duoap_skey` variable. | str | no |  |  |
| duoap_dirsync_api_host | The FQDN of the DUO API server for directory synchronization. If not specified, the role will use the `duoap_api_host` variable. | str | no |  |  |
| duoap_dirsync_service_account_username | The username of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory for directory synchronization. If not specified, the role will use the `duoap_service_account_username` variable. | str | no |  |  |
| duoap_dirsync_service_account_password | The password of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory for directory synchronization. If not specified, the role will use the `duoap_service_account_password` variable. | str | no |  |  |
| duoap_configure_sso | Whether the role will configure SSO. | bool | no |  | false |
| duoap_rikey | The integration key for SSO. If `duoap_configure_sso` is `true`, this variable is required. | str | no |  |  |
| duoap_sso_service_account_username | The username of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory for SSO. If not specified, the role will use the `duoap_service_account_username` variable. | str | no |  |  |
| duoap_sso_service_account_password | The password of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory for SSO. If not specified, the role will use the `duoap_service_account_password` variable. | str | no |  |  |
| duoap_logrotate_period | The period for log rotation. | str | no | <ul><li>daily</li><li>weekly</li><li>monthly</li></ul> | daily |
| duoap_logrotate_retention | The number of log files to retain. | int | no |  | 7 |
| duoap_configure_firewalld | Whether the role will configure firewalld. If Red Hat based or Debian, this will default to `true`. | bool | no |  | true |
| duoap_configure_ufw | Whether the role will configure ufw. If Ubuntu based, this will default to `true`. | bool | no |  | true |

### Options for duoap_combine_certs
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| files | A list of certificate files to combine. | list of 'path' | yes |  |  |
| path | The path to which the combined certificate will be written. | path | yes |  |  |

### Options for duoap_ad_clients
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | A comment with which to mark the AD client. | str | no |  |  |
| hosts | A list of hostnames or IP addresses to which to connect. | list of 'str' | yes |  |  |
| service_account_username | The username of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory. The `duoap_service_account_username` variable will be used if not specified. | str | no |  |  |
| service_account_password | The password of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory. The `duoap_service_account_password` variable will be used if not specified. | str | no |  |  |
| search_dn | The distinguished name of the search base. | str | yes |  |  |
| security_group_dn | The distinguished name of the security group of which membership is required to login. If not specified, no security group will be required. | str | no |  |  |
| ldap_filter | An LDAP filter that the users must match to login. | str | no |  |  |
| transport | The transport protocol to use. | str | no | <ul><li>clear</li><li>ldaps</li><li>starttls</li></ul> |  |
| timeout | The timeout in seconds for the connection before failing over to the next host. | int | no |  |  |
| ssl_ca_certs_file | The path to a file containing CA certificates to trust when making SSL connections. If not specified, the role will use the system default. | path | no |  |  |
| ssl_verify_hostname | Whether to verify the hostname of the SSL certificate. | bool | no |  | true |
| auth_type | The authentication type to use. If not specified, the role will use `ntlm2`. | str | no | <ul><li>ntlm2</li><li>plain</li></ul> |  |
| bind_dn | The distinguished name of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory. | str | no |  |  |
| ntlm_domain | The domain to use for NTLM authentication. | str | no |  |  |
| ntlm_workstation | The workstation to use for NTLM authentication. | str | no |  |  |
| port | The port on which to connect. | int | no |  |  |
| username_attribute | The attribute to use as the username. If not specified, the role will use `sAMAccountName`. | str | no |  |  |
| at_attribute | The attribute to use to match usernames with `@` symbol. If not specified, the role will use `userPrincipalName`. | str | no |  |  |

### Options for duoap_radius_clients
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | A comment with which to mark the RADIUS client. | str | no |  |  |
| hosts | A list of hostnames or IP addresses to which to connect. | list of 'str' | yes |  |  |
| secret | The shared secret to use for authentication. | str | yes |  |  |
| ports | A list of ports on which to connect. | list of 'int' | yes |  |  |
| retries | The number of times to retry connecting to the RADIUS server. | int | no |  |  |
| retry_wait | The number of seconds to wait between retries. | int | no |  |  |
| nas_ip | The IP address of the NAS. | str | no |  |  |
| pass_through_attr_names | A list of attributes to pass through to the RADIUS server. | list of 'str' | no |  |  |
| pw_codec | The codec to use for the password. | str | no |  |  |

### Options for duoap_ldap_auto_servers
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | A comment with which to mark the LDAP auto server. | str | no |  |  |
| ikey | The integration key for the DUO Authentication Proxy. | str | yes |  |  |
| skey | The secret key for the DUO Authentication Proxy. | str | yes |  |  |
| api_host | The FQDN of the DUO API server. | str | yes |  |  |
| client | The client ID for the DUO Authentication Proxy. | str | yes |  |  |
| factors | A list of factors to use for authentication. | list of 'str' | no | <ul><li>auto</li><li>push</li><li>phone</li><li>passcode</li></ul> |  |
| failmode | The failmode to use for authentication. | str | no | <ul><li>safe</li><li>secure</li></ul> |  |
| port | The port on which to listen for LDAP. | int | no |  |  |
| interface | The network interface on which to listen for LDAP. | str | no |  |  |
| api_timeout | The timeout in seconds for the API connection. If not specified, there is no timeout. | int | no |  |  |
| network_timeout | The timeout in seconds for the network connection. If not specified, the role will default to 10 minutes (600). | int | no |  |  |
| idle_timeout | The timeout in seconds for the idle connection. If not specified, the role will default to 1 hour (3600). | int | no |  |  |
| ssl_port | The port on which to listen for SSL. | int | no |  |  |
| ssl_key_path | The path to the SSL key file. | path | no |  |  |
| ssl_cert_path | The path to the SSL certificate file. | path | no |  |  |
| exempt_primary_bind | Whether to exempt the primary bind from DUO authentication. | bool | no |  | false |
| exempt_ous | A list of OUs to exempt from DUO authentication. | list of 'str' | no |  |  |
| delimiter | The delimiter to separate the password and the passcode in the password field. If not specified, the role will default to `,`. | str | no |  |  |
| delimiter_password_length | The length of the password in the password field. All characters after this length will be considered the passcode. | int | no |  |  |
| allow_concat | Whether to allow concatenation of the password and passcode. | bool | no |  | false |
| allow_searches_after_bind | Whether to allow searches after the primary bind. | bool | no |  | false |
| allow_unlimited_binds | Whether to allow unlimited binds. | bool | no |  | false |
| minimum_tls_version | The minimum TLS version to accept. | str | no | <ul><li>ssl3</li><li>tls1.0</li><li>tls1.1</li><li>tls1.2</li></ul> |  |
| cipher_list | The list of ciphers to accept. These are in OpenSSL format. https://www.openssl.org/docs/man1.1.1/man1/ciphers.html#CIPHER-LIST-FORMAT | str | no |  |  |

### Options for duoap_radius_auto_servers
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | A comment with which to mark the RADIUS auto server. | str | no |  |  |
| ikey | The integration key for the DUO Authentication Proxy. | str | yes |  |  |
| skey | The secret key for the DUO Authentication Proxy. | str | yes |  |  |
| api_host | The FQDN of the DUO API server. | str | yes |  |  |
| client | The client ID for the DUO Authentication Proxy. | str | yes |  |  |
| radius_clients | A list of RADIUS clients to use. | list of dicts of 'radius_clients' options | yes |  |  |
| factors | A list of factors to use for authentication. | list of 'str' | no | <ul><li>auto</li><li>push</li><li>phone</li><li>passcode</li></ul> |  |
| delimiter | The delimiter to separate the password and the passcode in the password field. If not specified, the role will default to `,`. | str | no |  |  |
| delimiter_password_length | The length of the password in the password field. All characters after this length will be considered the passcode. | int | no |  |  |
| allow_concat | Whether to allow concatenation of the password and passcode. | bool | no |  | false |
| api_timeout | The timeout in seconds for the API connection. If not specified, there is no timeout. | int | no |  |  |
| failmode | The failmode to use for authentication. | str | no | <ul><li>safe</li><li>secure</li></ul> |  |
| port | The port on which to listen for LDAP. | int | no |  |  |
| interface | The network interface on which to listen for LDAP. | str | no |  |  |
| pass_through_attr_names | A list of attributes to pass through to the RADIUS server. | list of 'str' | no |  |  |
| pass_through_all | Whether to pass through all attributes to the RADIUS server. | bool | no |  | false |
| client_ip_attr | The attribute to use for the client IP address. | str | no |  |  |
| exempt_usernames | A list of usernames to exempt from DUO authentication. | list of 'str' | no |  |  |
| pw_codec | The codec to use for the password. | str | no |  |  |

### Options for duoap_radius_auto_servers > radius_clients
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| ip | The IP address of the RADIUS client. | str | yes |  |  |
| secret | The shared secret to use for authentication. | str | yes |  |  |


## License
MIT

## Author and Project Information
Jim Tarpley
<!-- END_ANSIBLE_DOCS -->
