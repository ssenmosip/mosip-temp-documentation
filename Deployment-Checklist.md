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
            <td rowspan=2>L2 Name B</td>
            <td>L3 Name C</td>
        </tr>
        <tr>
            <td>L3 Name D</td>
        </tr>
    </tbody>
</table>

