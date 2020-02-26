# Oracle WebLogic

> All tips are for a Linux environment.

&nbsp;

Activate the debug mode permanently on a local domain:
- open the `setDomainEnv.sh` file for the domain
- locate and uncomment the following lines:
```
debugFlag="true"
export debugFlag
```
