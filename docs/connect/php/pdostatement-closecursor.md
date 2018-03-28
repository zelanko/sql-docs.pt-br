---
title: PDOStatement::closeCursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8997ab61-e948-4d54-8d32-fc080d55525c
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 46f2ec56126f4c0ed03a2928671f3b32bfd4270c
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="pdostatementclosecursor"></a>PDOStatement::closeCursor
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Fecha o cursor, permitindo que a instrução seja executada novamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
bool PDOStatement::closeCursor();  
```  
  
## <a name="return-value"></a>Valor de retorno  
true se bem-sucedido; caso contrário, false.  
  
## <a name="remarks"></a>Remarks  
closeCursor tem efeito quando a opção de conexão MultipleActiveResultSets está definida como false.  Para obter mais informações sobre a opção de conexão MultipleActiveResultSets, consulte [como: desabilitar vários Active Resultsets (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md).  
  
Em vez de chamar closeCursor, você pode apenas definir o identificador de instrução como nulo.  
  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
  
```  
<?php  
$database = "AdventureWorks";  
$server = "(local)";  
$conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "", array('MultipleActiveResultSets' => false ) );  
  
$stmt = $conn->prepare('SELECT * FROM Person.ContactType');  
  
$stmt2 = $conn->prepare('SELECT * FROM HumanResources.Department');  
  
$stmt->execute();  
  
$result = $stmt->fetch();  
print_r($result);  
  
$stmt->closeCursor();  
  
$stmt2->execute();  
$result = $stmt2->fetch();  
print_r($result);  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
