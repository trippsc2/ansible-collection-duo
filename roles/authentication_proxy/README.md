<!-- BEGIN_ANSIBLE_DOCS -->

# Ansible Role: trippsc2.duo.authentication_proxy
Version: 1.0.2

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
| duoap_configure_selinux | <p>Whether the role will configure SELinux for the DUO Authentication Proxy.</p> | bool | no |  | true |
| duoap_group | <p>The primary group of the `duoap_user` user under which the DUO Authentication Proxy will run.</p> | str | no |  | duo_authproxy_svc |
| duoap_user | <p>The user account as which the DUO Authentication Proxy will run.</p> | str | no |  | duo_authproxy_svc |
| duoap_combine_certs | <p>A list of dictionaries specifying the certificates to combine and the path to which they will be written.</p> | list of dicts of 'duoap_combine_certs' options | no |  |  |
| duoap_base_install_path | <p>The base path where the DUO Authentication Proxy will be installed.</p><p>The installed version will be placed at `./duoauthproxy-<version>` relative to this path.</p><p>A symlink will be created at `./duoauthproxy` pointing to the most recently installed version.</p> | path | no |  | /opt |
| duoap_version | <p>The version of the DUO Authentication Proxy to install.</p><p>If not specified, the latest version will be installed.</p><p>If another version is already installed and `duoap_upgrade` is set to `false`, the role will not upgrade/downgrade to this version.</p> | str | no |  |  |
| duoap_upgrade | <p>Whether the role will upgrade/downgrade the DUO Authentication Proxy to the specified version, if it is not already installed.</p> | bool | no |  | false |
| duoap_temp_path | <p>The path where temporary files will be stored during the installation process.</p> | path | no |  | /tmp/duoap |
| duoap_cleanup_old_version | <p>Whether the role will remove old versions of the DUO Authentication Proxy after upgrading/downgrading.</p> | bool | no |  | false |
| duoap_log_dir | <p>The directory where DUO Authentication Proxy logs will be stored.</p> | path | no |  | /var/log/duo |
| duoap_configure_logrotate | <p>Whether the role will configure logrotate for the DUO Authentication Proxy.</p> | bool | no |  | true |
| duoap_debug | <p>Whether DUO Authentication Proxy will run in debug mode.</p> | bool | no |  | false |
| duoap_log_auth_events | <p>Whether DUO Authentication Proxy will log authentication events.</p> | bool | no |  | false |
| duoap_log_sso_events | <p>Whether DUO Authentication Proxy will log SSO events.</p> | bool | no |  | false |
| duoap_log_max_files | <p>The maximum number of log files to keep.</p><p>If `duoap_configure_logrotate` is `true`, this will default to 0.</p> | int | no |  | 6 |
| duoap_log_max_size_in_mb | <p>The maximum size of each log file in megabytes.</p><p>If `duoap_configure_logrotate` is `true`, this will default to 0.</p> | int | no |  | 10 |
| duoap_http_ca_certs_file | <p>The path to a file containing CA certificates to trust when making HTTP requests.</p><p>If not specified, the role will use the system default.</p> | path | no |  | OS specific |
| duoap_interface | <p>The network interface on which the DUO Authentication Proxy will listen.</p> | str | no |  |  |
| duoap_http_proxy_host | <p>The hostname of the HTTP proxy server.</p> | str | no |  |  |
| duoap_http_proxy_port | <p>The port of the HTTP proxy server.</p> | int | no |  |  |
| duoap_test_connectivity_on_startup | <p>Whether the DUO Authentication Proxy will test connectivity to the DUO API server on startup.</p> | bool | no |  | false |
| duoap_service_account_username | <p>The username of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory.</p> | str | no |  |  |
| duoap_service_account_password | <p>The password of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory.</p> | str | no |  |  |
| duoap_ikey | <p>The integration key for the DUO Authentication Proxy.</p> | str | no |  |  |
| duoap_skey | <p>The secret key for the DUO Authentication Proxy.</p> | str | no |  |  |
| duoap_api_host | <p>The FQDN of the DUO API server.</p> | str | no |  |  |
| duoap_ad_clients | <p>A list of dictionaries specifying Active Directory clients.</p> | list of dicts of 'duoap_ad_clients' options | no |  |  |
| duoap_radius_clients | <p>A list of dictionaries specifying RADIUS clients.</p> | list of dicts of 'duoap_radius_clients' options | no |  |  |
| duoap_duo_only_client_enabled | <p>Whether the DUO Authentication Proxy will only allow DUO authentication.</p> | bool | no |  | false |
| duoap_ldap_auto_servers | <p>A list of dictionaries specifying LDAP auto servers.</p> | list of dicts of 'duoap_ldap_auto_servers' options | no |  |  |
| duoap_radius_auto_servers | <p>A list of dictionaries specifying RADIUS auto servers.</p> | list of dicts of 'duoap_radius_auto_servers' options | no |  |  |
| duoap_configure_dirsync | <p>Whether the role will configure directory synchronization.</p> | bool | no |  | false |
| duoap_dirsync_ikey | <p>The integration key for directory synchronization.</p><p>If not specified, the role will use the `duoap_ikey` variable.</p> | str | no |  |  |
| duoap_dirsync_skey | <p>The secret key for directory synchronization.</p><p>If not specified, the role will use the `duoap_skey` variable.</p> | str | no |  |  |
| duoap_dirsync_api_host | <p>The FQDN of the DUO API server for directory synchronization.</p><p>If not specified, the role will use the `duoap_api_host` variable.</p> | str | no |  |  |
| duoap_dirsync_service_account_username | <p>The username of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory for directory synchronization.</p><p>If not specified, the role will use the `duoap_service_account_username` variable.</p> | str | no |  |  |
| duoap_dirsync_service_account_password | <p>The password of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory for directory synchronization.</p><p>If not specified, the role will use the `duoap_service_account_password` variable.</p> | str | no |  |  |
| duoap_configure_sso | <p>Whether the role will configure SSO.</p> | bool | no |  | false |
| duoap_rikey | <p>The integration key for SSO.</p><p>If `duoap_configure_sso` is `true`, this variable is required.</p> | str | no |  |  |
| duoap_sso_service_account_username | <p>The username of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory for SSO.</p><p>If not specified, the role will use the `duoap_service_account_username` variable.</p> | str | no |  |  |
| duoap_sso_service_account_password | <p>The password of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory for SSO.</p><p>If not specified, the role will use the `duoap_service_account_password` variable.</p> | str | no |  |  |
| duoap_logrotate_period | <p>The period for log rotation.</p> | str | no | <ul><li>daily</li><li>weekly</li><li>monthly</li></ul> | daily |
| duoap_logrotate_retention | <p>The number of log files to retain.</p> | int | no |  | 7 |
| duoap_configure_firewalld | <p>Whether the role will configure firewalld.</p><p>For EL or Debian systems, this will default to true.</p><p>For Ubuntu systems, this will default to false.</p> | bool | no |  | true |
| duoap_configure_ufw | <p>Whether the role will configure ufw.</p><p>For Ubuntu systems, this will default to true.</p><p>For EL or Debian systems, this will default to false.</p> | bool | no |  | true |

### Options for duoap_combine_certs
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| files | <p>A list of certificate files to combine.</p> | list of 'path' | yes |  |  |
| path | <p>The path to which the combined certificate will be written.</p> | path | yes |  |  |

### Options for duoap_ad_clients
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | <p>A comment with which to mark the AD client.</p> | str | no |  |  |
| hosts | <p>A list of hostnames or IP addresses to which to connect.</p> | list of 'str' | yes |  |  |
| service_account_username | <p>The username of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory.</p><p>The `duoap_service_account_username` variable will be used if not specified.</p> | str | no |  |  |
| service_account_password | <p>The password of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory.</p><p>The `duoap_service_account_password` variable will be used if not specified.</p> | str | no |  |  |
| search_dn | <p>The distinguished name of the search base.</p> | str | yes |  |  |
| security_group_dn | <p>The distinguished name of the security group of which membership is required to login.</p><p>If not specified, no security group will be required.</p> | str | no |  |  |
| ldap_filter | <p>An LDAP filter that the users must match to login.</p> | str | no |  |  |
| transport | <p>The transport protocol to use.</p> | str | no | <ul><li>clear</li><li>ldaps</li><li>starttls</li></ul> |  |
| timeout | <p>The timeout in seconds for the connection before failing over to the next host.</p> | int | no |  |  |
| ssl_ca_certs_file | <p>The path to a file containing CA certificates to trust when making SSL connections.</p><p>If not specified, the role will use the system default.</p> | path | no |  |  |
| ssl_verify_hostname | <p>Whether to verify the hostname of the SSL certificate.</p> | bool | no |  | true |
| auth_type | <p>The authentication type to use.</p><p>If not specified, the role will use `ntlm2`.</p> | str | no | <ul><li>ntlm2</li><li>plain</li></ul> |  |
| bind_dn | <p>The distinguished name of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory.</p> | str | no |  |  |
| ntlm_domain | <p>The domain to use for NTLM authentication.</p> | str | no |  |  |
| ntlm_workstation | <p>The workstation to use for NTLM authentication.</p> | str | no |  |  |
| port | <p>The port on which to connect.</p> | int | no |  |  |
| username_attribute | <p>The attribute to use as the username.</p><p>If not specified, the role will use `sAMAccountName`.</p> | str | no |  |  |
| at_attribute | <p>The attribute to use to match usernames with `@` symbol.</p><p>If not specified, the role will use `userPrincipalName`.</p> | str | no |  |  |

### Options for duoap_radius_clients
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | <p>A comment with which to mark the RADIUS client.</p> | str | no |  |  |
| hosts | <p>A list of hostnames or IP addresses to which to connect.</p> | list of 'str' | yes |  |  |
| secret | <p>The shared secret to use for authentication.</p> | str | yes |  |  |
| ports | <p>A list of ports on which to connect.</p> | list of 'int' | yes |  |  |
| retries | <p>The number of times to retry connecting to the RADIUS server.</p> | int | no |  |  |
| retry_wait | <p>The number of seconds to wait between retries.</p> | int | no |  |  |
| nas_ip | <p>The IP address of the NAS.</p> | str | no |  |  |
| pass_through_attr_names | <p>A list of attributes to pass through to the RADIUS server.</p> | list of 'str' | no |  |  |
| pw_codec | <p>The codec to use for the password.</p> | str | no |  |  |

### Options for duoap_ldap_auto_servers
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | <p>A comment with which to mark the LDAP auto server.</p> | str | no |  |  |
| ikey | <p>The integration key for the DUO Authentication Proxy.</p> | str | yes |  |  |
| skey | <p>The secret key for the DUO Authentication Proxy.</p> | str | yes |  |  |
| api_host | <p>The FQDN of the DUO API server.</p> | str | yes |  |  |
| client | <p>The client ID for the DUO Authentication Proxy.</p> | str | yes |  |  |
| factors | <p>A list of factors to use for authentication.</p> | list of 'str' | no | <ul><li>auto</li><li>push</li><li>phone</li><li>passcode</li></ul> |  |
| failmode | <p>The failmode to use for authentication.</p> | str | no | <ul><li>safe</li><li>secure</li></ul> |  |
| port | <p>The port on which to listen for LDAP.</p> | int | no |  |  |
| interface | <p>The network interface on which to listen for LDAP.</p> | str | no |  |  |
| api_timeout | <p>The timeout in seconds for the API connection.</p><p>If not specified, there is no timeout.</p> | int | no |  |  |
| network_timeout | <p>The timeout in seconds for the network connection.</p><p>If not specified, the role will default to 10 minutes (600).</p> | int | no |  |  |
| idle_timeout | <p>The timeout in seconds for the idle connection.</p><p>If not specified, the role will default to 1 hour (3600).</p> | int | no |  |  |
| ssl_port | <p>The port on which to listen for SSL.</p> | int | no |  |  |
| ssl_key_path | <p>The path to the SSL key file.</p> | path | no |  |  |
| ssl_cert_path | <p>The path to the SSL certificate file.</p> | path | no |  |  |
| exempt_primary_bind | <p>Whether to exempt the primary bind from DUO authentication.</p> | bool | no |  | false |
| exempt_ous | <p>A list of OUs to exempt from DUO authentication.</p> | list of 'str' | no |  |  |
| delimiter | <p>The delimiter to separate the password and the passcode in the password field.</p><p>If not specified, the role will default to `,`.</p> | str | no |  |  |
| delimiter_password_length | <p>The length of the password in the password field.</p><p>All characters after this length will be considered the passcode.</p> | int | no |  |  |
| allow_concat | <p>Whether to allow concatenation of the password and passcode.</p> | bool | no |  | false |
| allow_searches_after_bind | <p>Whether to allow searches after the primary bind.</p> | bool | no |  | false |
| allow_unlimited_binds | <p>Whether to allow unlimited binds.</p> | bool | no |  | false |
| minimum_tls_version | <p>The minimum TLS version to accept.</p> | str | no | <ul><li>ssl3</li><li>tls1.0</li><li>tls1.1</li><li>tls1.2</li></ul> |  |
| cipher_list | <p>The list of ciphers to accept.</p><p>These are in OpenSSL format. https://www.openssl.org/docs/man1.1.1/man1/ciphers.html#CIPHER-LIST-FORMAT</p> | str | no |  |  |

### Options for duoap_radius_auto_servers
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | <p>A comment with which to mark the RADIUS auto server.</p> | str | no |  |  |
| ikey | <p>The integration key for the DUO Authentication Proxy.</p> | str | yes |  |  |
| skey | <p>The secret key for the DUO Authentication Proxy.</p> | str | yes |  |  |
| api_host | <p>The FQDN of the DUO API server.</p> | str | yes |  |  |
| client | <p>The client ID for the DUO Authentication Proxy.</p> | str | yes |  |  |
| radius_clients | <p>A list of RADIUS clients to use.</p> | list of dicts of 'radius_clients' options | yes |  |  |
| factors | <p>A list of factors to use for authentication.</p> | list of 'str' | no | <ul><li>auto</li><li>push</li><li>phone</li><li>passcode</li></ul> |  |
| delimiter | <p>The delimiter to separate the password and the passcode in the password field.</p><p>If not specified, the role will default to `,`.</p> | str | no |  |  |
| delimiter_password_length | <p>The length of the password in the password field.</p><p>All characters after this length will be considered the passcode.</p> | int | no |  |  |
| allow_concat | <p>Whether to allow concatenation of the password and passcode.</p> | bool | no |  | false |
| api_timeout | <p>The timeout in seconds for the API connection.</p><p>If not specified, there is no timeout.</p> | int | no |  |  |
| failmode | <p>The failmode to use for authentication.</p> | str | no | <ul><li>safe</li><li>secure</li></ul> |  |
| port | <p>The port on which to listen for LDAP.</p> | int | no |  |  |
| interface | <p>The network interface on which to listen for LDAP.</p> | str | no |  |  |
| pass_through_attr_names | <p>A list of attributes to pass through to the RADIUS server.</p> | list of 'str' | no |  |  |
| pass_through_all | <p>Whether to pass through all attributes to the RADIUS server.</p> | bool | no |  | false |
| client_ip_attr | <p>The attribute to use for the client IP address.</p> | str | no |  |  |
| exempt_usernames | <p>A list of usernames to exempt from DUO authentication.</p> | list of 'str' | no |  |  |
| pw_codec | <p>The codec to use for the password.</p> | str | no |  |  |

### Options for duoap_radius_auto_servers > radius_clients
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| ip | <p>The IP address of the RADIUS client.</p> | str | yes |  |  |
| secret | <p>The shared secret to use for authentication.</p> | str | yes |  |  |


## License
MIT

## Author and Project Information
Jim Tarpley
<!-- END_ANSIBLE_DOCS -->
