
### Deployment Checklist
This checklist should be verified once the environment is ready, and before it can be consumed.

Deployment checklist is divided into 2 parts - 
 1. `Infrastructure Checklist` – This checklist lists the required installations for all the modules.
 2. `Application Checklist` – This checklist lists the dependent services, configurations, required roles, any explicit permissions, etc. for all the modules.

***1. Infrastructure Checklist***    
<table>
    <thead>
        <tr>
            <th>Module Name</th>
            <th>Infrastructure Checklist</th>
            <th>Additional Information</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td rowspan=5>Kernel</td>
            <td rowspan=1>PostgreSQL</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=1>SMTP Server</td>
            <td>If mail notification is enabled</td>
        </tr>
        <tr>
            <td rowspan=1>SMS Gateway</td>
            <td>If SMS notification is enabled</td>
        </tr>
        <tr>
            <td rowspan=1>HDFS</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=1>LDAP</td>
            <td>Import ldif</td>
        </tr>
       <tr>
            <td rowspan=5>Pre-Registration</td>
            <td rowspan=1>PostgreSQL</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=1>SMTP Server</td>
            <td>If mail notification is enabled</td>
        </tr>
        <tr>
            <td rowspan=1>SMS Gateway</td>
            <td>If SMS notification is enabled</td>
        </tr>
        <tr>
            <td rowspan=1>HDFS</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=1>LDAP</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=5>Registration</td>
            <td rowspan=1>TPM</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=1>SMTP Server</td>
            <td>If mail notification is enabled</td>
        </tr>
        <tr>
            <td rowspan=1>SMS Gateway</td>
            <td>If SMS notification is enabled</td>
        </tr>
        <tr>
            <td rowspan=1>Devices</td>
            <td>Fingerprint Slab, Iris, Webcamera, Printer, Scanner</td>
        </tr>
        <tr>
            <td rowspan=1>LDAP</td>
            <td></td>
        </tr>
     <tr>
            <td rowspan=7>Registration Processor</td>
            <td rowspan=1>Virus Scanner</td>
            <td>ClamAV virusscanner service should be accessible from dmz and secure zone using IP:Port</td>
        </tr>
        <tr>
            <td rowspan=1>SMTP Server</td>
            <td>If mail notification is enabled</td>
        </tr>
        <tr>
            <td rowspan=1>SMS Gateway</td>
            <td>If SMS notification is enabled</td>
        </tr>
        <tr>
            <td rowspan=1>HDFS</td>
            <td>HDFS should be accessible, and write permission to regproc user should be provided</td>
        </tr>
        <tr>
            <td rowspan=1>ActiveMQ</td>
            <td>ActiveMQ should be installed and accessible using IP:Port</td>
        </tr>
         <tr>
            <td rowspan=1>LDAP</td>
            <td></td>
        </tr>
         <tr>
            <td rowspan=1>PostgresSQL</td>
            <td></td>
        </tr>
       <tr>
            <td rowspan=3>ID Repository</td>
            <td rowspan=1>HDFS</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=1>LDAP</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=1>PostgresSQL</td>
            <td></td>
        </tr>
       <tr>
            <td rowspan=4>ID Authentication</td>
            <td rowspan=1>SMTP Server</td>
            <td>If mail notification is enabled</td>
        </tr>
        <tr>
            <td rowspan=1>SMS Gateway</td>
            <td>If SMS notification is enabled</td>
        </tr>
        <tr>
            <td rowspan=1>LDAP</td>
            <td></td>
        </tr>
        <tr>
            <td rowspan=1>PostgresSQL</td>
            <td></td>
        </tr>    
    </tbody>
</table>




