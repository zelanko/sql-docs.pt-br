---
title: 'Pdostatement:: ErrorInfo | Microsoft Docs'
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
ms.topic: article
ms.assetid: e45bebe8-ea4c-49b6-93db-cf1ae65f530c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ec0f059e1be3cf476faa2ac4ff0b4f71c7643511
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MTE
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="pdostatementerrorinfo"></a>PDOStatement::errorInfo
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Recupera informações de erro estendidas da operação mais recente no identificador da instrução.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
array PDOStatement::errorInfo();  
```  
  
## <a name="return-value"></a>Valor retornado  
Uma matriz de informações de erro sobre a operação mais recente no identificador da instrução. A matriz consiste nos seguintes campos:  
  
-   O código de erro SQLSTATE  
  
-   O código de erro específico do driver  
  
-   A mensagem de erro específica do driver  
  
Se não houver nenhum erro ou se o SQLSTATE não for definido, os campos específicos do driver serão NULL.  
  
## <a name="remarks"></a>Remarks  
O suporte para PDO foi adicionado na versão 2.0 dos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="example"></a>Exemplo  
Neste exemplo, a instrução SQL tem um erro, que é relatado em seguida.  
  
```  
<?php  
$conn = new PDO( "sqlsrv:server=(local) ; Database = AdventureWorks", "", "");  
$stmt = $conn->prepare('SELECT * FROM Person.Addressx');  
  
$stmt->execute();  
print_r ($stmt->errorInfo());  
?>  
```  
  
## <a name="see-also"></a>Consulte Também  
[PDOStatement Class](../../connect/php/pdostatement-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
