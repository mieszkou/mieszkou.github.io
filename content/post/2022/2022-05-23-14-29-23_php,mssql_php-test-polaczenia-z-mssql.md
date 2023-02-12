---
title: "PHP: test połączenia z MSSQL"
description: "Jak sprawdzić czy działa połączenie z MSSQL"
image: /img/2023-02-12-23-01-39.png
date: 2022-05-23
hidden: false
comments: true
draft: false
tags:
    - php
    - sql
    - tsql
    - mssql
    - programowanie
categories:
    - PHP
    - Programowanie

---





```php
<?php
$serverName = "127.0.0.1,1433"; //serverNameinstanceName, portNumber (default is 1433)
$connectionInfo = array( "Database"=>"demo", "UID"=>"sa", "PWD"=>"pass");
$conn = sqlsrv_connect( $serverName, $connectionInfo);

if( $conn ) {
     echo "Connection established.<br />";
}else{
     echo "Connection could not be established.<br />";
     die( print_r( sqlsrv_errors(), true));
}
?>
```