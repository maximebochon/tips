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

&nbsp;

Unlock a user account:
```sql
alter user _USER_ account unlock;
```

&nbsp;

Change a user's password:
```sql
alter user _USER_ identified by _NEW_PASSWORD_;
```

&nbsp;

Handle raw data:
```sql
create table raw_test (id numeric(6) not null, data raw(4), info varchar2(5));
alter table raw_test add constraint raw_test_pk primary key (id);

insert into raw_test (id, data, info) values (0, hextoraw('0011AAFF'), 'test0'); -- case insensitive
insert into raw_test (id, data, info) values (1, hextoraw('5A0D61F7'), 'test1'); -- case insensitive
insert into raw_test (id, data, info) values (2, hextoraw('0011aaff'), 'test2'); -- case insensitive
commit;

select * from raw_test where data <> hextoraw('0011aaff'); -- lowercase
-- 1 | 5A0D61F7 | test1 --

select * from raw_test where rawtohex(data) = '0011AAFF'; -- uppercase
-- 0 | 0011AAFF | test0 --
-- 2 | 0011AAFF | test2 --

select info, rawtohex(data), utl_raw.substr(data, 3, 1) from raw_test;
-- test0 | 0011AAFF | AA --
-- test1 | 5A0D61F7 | 61 --
-- test2 | 0011AAFF | AA --
```

&nbsp;

Make it easy to have multiple table tabs open at once in [SQL Developer](https://docs.oracle.com/en/database/oracle/sql-developer/index.html):
- Tools 🠖 Preferences...
- Database 🠖 Object Viewer
- Automatically Freeze Object Viewer Windows
