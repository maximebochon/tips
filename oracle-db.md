# Oracle Database notes

## SQL

Get current timestamp:
```sql
select to_char(sysdate, 'YYYY-MM-DD HH24:MI:SS') from dual;
-- output example: 2017-12-13 14:20:11
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

Add a comment on a column:
```sql
comment on column some_table.some_column is
'Description of column ''some_column'' to help developers and testers to use it.';
```

&nbsp;

Add extra checkings on column values:
```sql
-- Limit possible values of a VARCHAR2 column:
alter table t add constraint check_format check ( format in ( 'CSV', 'XML', 'JSON', 'RAW' ) );

-- Constrain precedence between two dates:
alter table t add constraint check_event check ( event_end is null or event_start <= event_end );

-- Restrict range of a NUMBER(1) column to map days of week:
alter table t add constraint check_day check ( day_of_week between 0 and 6 );

-- Enforce a CHAR(4) column to describe time values, using the two first digits for hours and the two last for minutes:
-- Valid examples: '0000', '0059', '1200', '1435', '2359'
alter table t add constraint check_hhmm check ( regexp_like( hhmm, '^([0-1][0-9]|[2][0-3])([0-5][0-9])$' ) );

-- Enforce a CHAR(36) column to describe a canonical textual representation of a 128 bits UUID:
alter table t add constraint check_uuid check ( regexp_like( uuid, '^[0-9a-f]{4}([0-9a-f]{4}-){4}[0-9a-z]{12}$' ) );
```

&nbsp;

## SQL\*Plus

Disconnect from SQL\*Plus when stuck: `CTRL+D`

&nbsp;

SQL\*Plus can work well with arrow keys by calling `sqlplus` through `rlwrap`:
```bash
sudo apt install rlwrap
sudo su oracle
rlwrap sqlplus
```

&nbsp;

## SQL Developer

Make it easy to have multiple table tabs open at once in [SQL Developer](https://docs.oracle.com/en/database/oracle/sql-developer/index.html):
- Tools 🠖 Preferences...
- Database 🠖 Object Viewer
- Automatically Freeze Object Viewer Windows

&nbsp;

Display connection passwords in [SQL Developer](https://docs.oracle.com/en/database/oracle/sql-developer/index.html):
- Install _TomeCode_'s _Show Me Password_ extension for SQL Developer:
  - Download [here](http://show-me-password.tomecode.com/) the extension archive targeting your version of SQL Developer.
  - Go to _Help_ 🠖 _Check for Updates..._
  - Choose _Install From Local Files(s)_ and point to the downloaded file.
  - Click _Next_ and _Finish_.
  - Restart SQL Developer.
- Go to _File_ 🠖 _Show Me Password_.
- Read column _Saved Password_.

&nbsp;

Force the user interface language to _English_ in [SQL Developer](https://docs.oracle.com/en/database/oracle/sql-developer/index.html):
- Edit file `sqldeveloper\bin\sqldeveloper.conf` in SQL Developer's installation directory.
- Add the following line and save: `AddVMOption -Duser.language=en`
