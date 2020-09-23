---
title: PDO::query
description: Referência da API para a função PDO::query no Driver PDO_SQLSRV da Microsoft para PHP para SQL Server.
ms.custom: ''
ms.date: 08/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f6f5e6d4-8ca9-4f06-89ed-de65ad3952a2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dfceb71c40b7214d9570a62c7ff65925b4f19849
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87410942"
---
# <a name="pdoquery"></a>PDO::query
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Executa uma consulta SQL e retorna um conjunto de resultados como um objeto PDOStatement.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
PDOStatement PDO::query ($statement[, $fetch_style);  
```  
  
#### <a name="parameters"></a>Parâmetros  
*$statement*: a instrução SQL que você quer executar.  
  
*$fetch_style*: as instruções opcionais sobre como executar a consulta. Para obter mais detalhes, consulte a seção Comentários. $*fetch_style* em PDO::query pode ser substituído por *$fetch_style* em PDO::fetch.  
  
## <a name="return-value"></a>Valor de retorno  
Se a chamada for bem-sucedida, o PDO::query retornará um objeto PDOStatement. Se a chamada falhar, PDO::query gerará um objeto PDOException ou retornará false, dependendo da configuração de PDO::ATTR_ERRMODE.  
  
## <a name="exceptions"></a>Exceções  
PDOException.  
  
## <a name="remarks"></a>Comentários  
Uma consulta executada com PDO::query pode executar uma instrução preparada ou de forma direta, dependendo da configuração de PDO::SQLSRV_ATTR_DIRECT_QUERY. Para obter mais informações, consulte [Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).  
  
PDO::SQLSRV_ATTR_QUERY_TIMEOUT também afeta o comportamento de PDO::exec, veja [PDO::setAttribute](../../connect/php/pdo-setattribute.md).  
  
Você pode especificar as seguintes opções para $*fetch_style*.  
  
|Estilo|Descrição|  
|---------|---------------|  
|PDO::FETCH_COLUMN, *num*|Consultas de dados na coluna especificada. A primeira coluna na tabela é a coluna 0.|  
|PDO::FETCH_CLASS, '*classname*', array( *arglist* )|Cria uma instância de uma classe e atribui nomes de coluna a propriedades da classe. Se o construtor de classe aceitar um ou mais parâmetros, você poderá passar também uma *arglist*.|  
|PDO::FETCH_CLASS, '*classname*'|Atribui nomes de coluna a propriedades de uma classe existente.|  
  
Chame PDOStatement::closeCursor para liberar os recursos de banco de dados associados ao objeto PDOStatement antes de chamar PDO::query novamente.  
  
Você pode fechar um objeto PDOStatement definindo-o como null.  
  
Se nem todos os dados de um conjunto de resultados forem buscados, a próxima chamada a PDO::query não falhará.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Este exemplo mostra várias consultas.  
  
```  
<?php  
$database = "AdventureWorks";  
$conn = new PDO( "sqlsrv:server=(local) ; Database = $database", "", "");  
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  
$conn->setAttribute( PDO::SQLSRV_ATTR_QUERY_TIMEOUT, 1 );  
  
$query = 'select * from Person.ContactType';  
  
// simple query  
$stmt = $conn->query( $query );  
while ( $row = $stmt->fetch( PDO::FETCH_ASSOC ) ){  
   print_r( $row['Name'] ."\n" );  
}  
  
echo "\n........ query for a column ............\n";  
  
// query for one column  
$stmt = $conn->query( $query, PDO::FETCH_COLUMN, 1 );  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query with a new class ............\n";  
$query = 'select * from HumanResources.Department order by GroupName';  
// query with a class  
class cc {  
   function __construct( $arg ) {  
      echo "$arg";  
   }  
  
   function __toString() {  
      return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
   }  
}  
  
$stmt = $conn->query( $query, PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
  
while ( $row = $stmt->fetch() ){  
   echo "$row\n";  
}  
  
echo "\n........ query into an existing class ............\n";  
$c_obj = new cc( '' );  
$stmt = $conn->query( $query, PDO::FETCH_INTO, $c_obj );  
while ( $stmt->fetch() ){  
   echo "$c_obj\n";  
}  
  
$stmt = null;  
?>  
```

## <a name="example"></a>Exemplo
Este exemplo de código mostra como criar uma tabela de tipos [sql_variant](https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql) tipos e buscar os dados inseridos.

```
<?php
$server = 'serverName';
$dbName = 'databaseName';
$uid = 'yourUserName';
$pwd = 'yourPassword';

$conn = new PDO("sqlsrv:server=$server; database = $dbName", $uid, $pwd);
$conn->setAttribute( PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION );  

try {
    $tableName = 'testTable';
    $query = "CREATE TABLE $tableName ([c1_int] sql_variant, [c2_varchar] sql_variant)";

    $stmt = $conn->query($query);
    unset($stmt);

    $query = "INSERT INTO [$tableName] (c1_int, c2_varchar) VALUES (1, 'test_data')";
    $stmt = $conn->query($query);
    unset($stmt);

    $query = "SELECT * FROM $tableName";
    $stmt = $conn->query($query);

    $result = $stmt->fetch(PDO::FETCH_ASSOC);
    print_r($result);
    
    unset($stmt);
    unset($conn);
} catch (Exception $e) {
    echo $e->getMessage();
}
?>
```

A saída esperada seria:

```
Array
(
    [c1_int] => 1
    [c2_varchar] => test_data
)
```

## <a name="see-also"></a>Consulte Também  
[PDO Class](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
