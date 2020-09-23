---
title: Como recuperar tipos de data e hora como objetos DateTime do PHP usando o Driver PDO_SQLSRV
description: Este tópico descreve como recuperar tipos de data e hora como objetos DateTime do PHP ao usar o Driver PDO_SQLSRV da Microsoft para PHP para SQL Server
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date and time types, retrieving as datetime objects
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 507dc2a228419fb695d10a437681229ec6586f11
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680751"
---
# <a name="how-to-retrieve-date-and-time-types-as-php-datetime-objects-using-the-pdo_sqlsrv-driver"></a>Como recuperar tipos de data e hora como objetos DateTime PHP usando o driver PDO_SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Esse recurso, adicionado na versão 5.6.0, é válido somente ao usar o driver PDO_SQLSRV para o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].

### <a name="to-retrieve-date-and-time-types-as-datetime-objects"></a>Para recuperar tipos de data e hora como objetos DateTime

Ao usar os tipos PDO_SQLSRV, os tipos de data e hora (**smalldatetime**, **datetime**, **date**, **time**, **datetime2** e **datetimeoffset**) são retornados por padrão como cadeias de caracteres. Nem o atributo PDO::ATTR_STRINGIFY_FETCHES nem o PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE tem qualquer efeito. Para recuperar os tipos de data e hora como objetos [PHP DateTime](http://php.net/manual/en/class.datetime.php), defina o atributo de conexão ou instrução `PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE` como **true** (ele é **false** por padrão).

> [!NOTE]
> Este atributo de conexão ou instrução só se aplica à busca regular de tipos de data e hora porque os objetos DateTime não podem ser especificados como parâmetros de saída.

## <a name="example---use-the-connection-attribute"></a>Exemplo – usar o atributo de conexão
Os exemplos a seguir omitem a verificação de erros para maior clareza. Este mostra como definir o atributo de conexão:

```php
<?php
$server = 'myserver';
$databaseName = 'mydatabase';
$username = 'myusername';
$passwd = 'mypasword';
$tableName = 'mytable';

$conn = new PDO("sqlsrv:Server = $server; Database = $databaseName", $username, $passwd);

// To set the connection attribute
$conn->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$query = "SELECT DateTimeCol FROM $tableName";
$stmt = $conn->prepare($query);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_ASSOC);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-attribute"></a>Exemplo – usar o atributo de instrução
Este exemplo mostra como definir o atributo de instrução:

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");
$query = "SELECT DateTimeCol FROM myTable";
$stmt = $conn->prepare($query);
$stmt->setAttribute(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE, true);
$stmt->execute();

// Expect a DateTimeCol value as a PHP DateTime type
$row = $stmt->fetch(PDO::FETCH_NUM);
var_dump($row);

unset($stmt);
unset($conn);
?>
```

## <a name="example---use-the-statement-option"></a>Exemplo – usar a opção de instrução
Como alternativa, o atributo de instrução pode ser definido como uma opção:

```php
<?php
$database = "test";
$server = "(local)";
$conn = new PDO("sqlsrv:server = $server; Database = $database", "", "");

$dateObj = null;
$query = "SELECT DateTimeCol FROM aTable";
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => true);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateObj, PDO::PARAM_LOB);
$row = $stmt->fetch(PDO::FETCH_BOUND);
var_dump($dateObj);

unset($stmt);
unset($conn);
?>
```

## <a name="example---retrieve-datetime-types-as-strings"></a>Exemplo – recuperar tipos datetime como cadeias de caracteres
O seguinte exemplo mostra como alcançar o oposto (que, na verdade, não é necessário porque ele é false por padrão):

```php
<?php
$database = "MyData";
$conn = new PDO("sqlsrv:server = (local); Database = $database");

$dateStr = null;
$query = 'SELECT DateTimeCol FROM table1';
$options = array(PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE => false);
$stmt = $conn->prepare($query, $options);
$stmt->execute();
$stmt->bindColumn(1, $dateStr);
$row = $stmt->fetch(PDO::FETCH_BOUND);
echo $dateStr . PHP_EOL;

unset($stmt);
unset($conn);
?>
```

## <a name="see-also"></a>Consulte Também
[Recuperando dados](../../connect/php/retrieving-data.md)

[Recuperar tipos de data e hora como cadeias de caracteres usando o driver SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)
