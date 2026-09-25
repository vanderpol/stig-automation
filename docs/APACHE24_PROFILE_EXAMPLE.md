# Apache 2.4 profile example

This is an explanatory example, not an approved production profile.

```yaml
# Required/site-approved values
apache24_stig_listen:
  - "192.0.2.20:443"

# Administrative ownership assessment
apache24_stig_approved_admin_accounts:
  - root
  - ansible
  - deploysvc

apache24_stig_admin_audit_paths:
  - /etc/httpd
  - /var/www

# Organization-defined network restrictions
apache24_stig_blocked_networks:
  - "192.0.2.0/24"

# Set only after application categorization
apache24_stig_session_timeout_minutes: 10

# Example site decision: CGI is not approved/required
apache24_stig_disable_cgi: true
apache24_stig_cgi_approved: false
```

The values above are placeholders. In particular, TEST-NET addresses are examples and must not be treated as organization-approved production values.
