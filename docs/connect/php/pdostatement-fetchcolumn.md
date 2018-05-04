---
title: PDOStatement::fetchColumn | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6ebf385c-ddb0-4c53-9dc6-7df0d3740b04
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbfd8ed8ff72708a7113785f4ba707d9e5b39f3d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="pdostatementfetchcolumn"></a>PDOStatement::fetchColumn
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Retorna uma coluna em uma linha.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
string PDOStatement::fetchColumn ([ $column_number ] );  
```  
  
#### <a name="parameters"></a>Parâmetros  
$*Núm_col*: um inteiro opcional que indica o número de coluna com base em zero. O padrão é 0 (a primeira coluna na linha).  
  
## <a name="return-value"></a>Valor de retorno  
Uma coluna ou false se não houver mais linhas.  
  
## <a name="remarks"></a>Remarks  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   while ( $result = $stmt->fetchColumn(1)) {   
      print($result . "\n");   
   }  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
