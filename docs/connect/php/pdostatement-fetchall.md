---
title: PDOStatement::fetchAll
description: Referência de API para a função PDOStatement::fetchAll no Driver do Microsoft PDO_SQLSRV para PHP para SQL Server.
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: be74188a-77cd-4d19-b16e-77278373c979
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c3ab50febea25e68b634d2f2afeb6a20b71bf82
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645092"
---
# <a name="pdostatementfetchall"></a>PDOStatement::fetchAll
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna as linhas em um conjunto de resultados em uma matriz.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
array PDOStatement::fetchAll([ $fetch_style[, $column_index ][, ctor_args]] );  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*fetch_style*: um símbolo (inteiro) que especifica o formato dos dados da linha. Consulte [PDOStatement::fetch](../../connect/php/pdostatement-fetch.md) para obter uma lista de valores. PDO::FETCH_COLUMN também é permitido. PDO::FETCH_BOTH é o padrão.  
  
$*column_index*: um valor inteiro que representa a coluna a ser retornada se $*fetch_style* for PDO::FETCH_COLUMN. 0 é o padrão.  
  
$*ctor_args*: uma matriz dos parâmetros para um construtor de classe quando $*fetch_style* é PDO::FETCH_CLASS ou PDO::FETCH_OBJ.  
  
## <a name="return-value"></a>Valor de retorno  
Uma matriz das linhas restantes do conjunto de resultados, ou false em caso de falha na chamada do método.  
  
## <a name="remarks"></a>Comentários  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   print "-----------\n";  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_BOTH);  
   print_r( $result );  
   print "\n-----------\n";  
  
   print "-----------\n";  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_NUM);  
   print_r( $result );  
   print "\n-----------\n";  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetchall(PDO::FETCH_COLUMN, 1);  
   print_r( $result );  
   print "\n-----------\n";  
  
   class cc {  
      function __construct( $arg ) {  
         echo "$arg\n";  
      }  
  
      function __toString() {  
         echo "To string\n";  
      }  
   };  
  
   $stmt = $conn->query( 'SELECT TOP(2) * FROM Person.ContactType' );  
   $all = $stmt->fetchAll( PDO::FETCH_CLASS, 'cc', array( 'Hi!' ));  
   var_dump( $all );  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
