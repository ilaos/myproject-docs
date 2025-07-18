# IP Whitelisting

## Overview

To ensure smooth operation of the AlmaSEO application without interference from ModSecurity or other security measures, you need to whitelist the application's IP address on your server.

## Why IP Whitelisting is Necessary

- **ModSecurity Bypass**: Prevents false positives from ModSecurity rules
- **Rate Limiting**: Avoids rate limiting restrictions
- **Security Headers**: Bypasses certain security header checks
- **Smooth Operation**: Ensures uninterrupted API calls and data processing

## Current IP Address

**Primary IP Address**: `[YOUR_SERVER_IP]`

> **Note**: Replace `[YOUR_SERVER_IP]` with your actual server IP address.

## Implementation Methods

### Method 1: Apache Configuration (Recommended)

Add the following to your Apache configuration or `.htaccess` file:

```apache
# IP Whitelisting for AlmaSEO
<IfModule mod_security.c>
    SecRule REMOTE_ADDR "@ipMatch [YOUR_SERVER_IP]" "id:1000,phase:1,pass,nolog,ctl:ruleEngine=Off"
</IfModule>

# Alternative method for specific paths
<Location "/api/">
    <IfModule mod_security.c>
        SecRule REMOTE_ADDR "@ipMatch [YOUR_SERVER_IP]" "id:1001,phase:1,pass,nolog,ctl:ruleEngine=Off"
    </IfModule>
</Location>
```

### Method 2: Nginx Configuration

If using Nginx, add to your server block:

```nginx
# IP Whitelisting for AlmaSEO
location / {
    # Allow specific IP
    allow [YOUR_SERVER_IP];
    deny all;
    
    # Your existing configuration here
    proxy_pass http://backend;
    # ... other directives
}
```

### Method 3: Cloudflare Configuration

If using Cloudflare, you can whitelist the IP in the Cloudflare dashboard:

1. Go to **Security** → **WAF**
2. Add a custom rule to allow your server IP
3. Set the rule to "Allow" for the specific IP address

## Verification

After implementing the whitelist, verify it's working by:

1. **Check Logs**: Monitor your server logs for any blocked requests
2. **Test API Calls**: Make test API calls to ensure they're not being blocked
3. **Monitor Performance**: Ensure smooth operation without security interruptions

## Security Considerations

- **Keep IP Updated**: If your server IP changes, update the whitelist immediately
- **Monitor Access**: Regularly check server logs for any unauthorized access attempts
- **Backup Configuration**: Keep backups of your configuration files
- **Documentation**: Maintain clear documentation of all whitelisted IPs

## Troubleshooting

### Common Issues

1. **Still Getting Blocked**: Ensure the IP address is correct and the configuration is properly loaded
2. **Configuration Not Applied**: Restart your web server after making changes
3. **Multiple IPs**: If you have multiple server IPs, add them all to the whitelist

### Testing Commands

```bash
# Test if your IP is being blocked
curl -I https://yourdomain.com/api/test

# Check server logs for ModSecurity activity
tail -f /var/log/apache2/error.log | grep ModSecurity
```

## Support

If you encounter issues with IP whitelisting:

1. Check your server's error logs
2. Verify the IP address is correct
3. Ensure the configuration syntax is valid
4. Contact support if problems persist

---

**Last Updated**: [Current Date]
**Version**: 1.0 