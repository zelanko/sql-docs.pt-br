---
title: PDOStatement::errorCode | Microsoft Docs
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
ms.assetid: 4161abec-c12b-444e-9de5-f1dac7b3e0e4
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5b241fe8af8cf2e7437568aa753d4a865cdf82bb
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="pdostatementerrorcode"></a>PDOStatement::errorCode
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera o SQLSTATE da operação mais recente no objeto de instrução do banco de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
string PDOStatement::errorCode();  
```  
  
## <a name="return-value"></a>Valor de retorno  
Retorna um SQLSTATE de cinco caracteres como uma cadeia de caracteres ou NULL se não houve nenhuma operação no identificador da instrução.  
  
## <a name="remarks"></a>Remarks  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Este exemplo mostra uma consulta SQL que tem um erro.  O código de erro é exibido.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print $stmt->errorCode();  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
