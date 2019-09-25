# Oracle notes

Get current timestamp:
```sql
select to_char(sysdate, 'YYYY-MM-DD HH24:MI:SS') from dual;
-- output example: 2017-12-13 14:20:11
```
&nbsp;

Disconnect from SQL\*Plus when stuck: `CTRL+D`

&nbsp;

SQL\*Plus can work well with arrow keys by calling `sqlplus` through `rlwrap`:
```bash
sudo apt install rlwrap
sudo su oracle
rlwrap sqlplus
```
