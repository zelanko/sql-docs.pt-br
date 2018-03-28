---
title: Direcionar instrução - preparado instrução execução PDO_SQLSRV Driver | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
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
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d7967e4f2c888ccdb90c56ac3b1504187b77b48a
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico discute o uso do atributo PDO:: sqlsrv_attr_direct_query para especificar a execução de instrução direta em vez do padrão, que é a execução da instrução preparada. Usar uma instrução preparada pode resultar em melhor desempenho se a instrução for executada mais de uma vez usando a associação de parâmetro.  
  
## <a name="remarks"></a>Remarks  
Se você quiser enviar um [!INCLUDE[tsql](../../includes/tsql_md.md)] instrução diretamente para o servidor sem preparação de instrução pelo driver, você pode definir o atributo PDO:: sqlsrv_attr_direct_query com [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) (ou como uma opção de driver passados para [PDO::__construct](../../connect/php/pdo-construct.md)) ou quando você chama [PDO](../../connect/php/pdo-prepare.md). Por padrão, o valor de PDO:: sqlsrv_attr_direct_query for False (use a execução da instrução preparada).  
  
Se você usar [PDO:: Query](../../connect/php/pdo-query.md), talvez você queira a execução direta. Antes de chamar [PDO:: Query](../../connect/php/pdo-query.md), chame [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) e defina PDO:: sqlsrv_attr_direct_query como True.  Cada chamada para [PDO:: Query](../../connect/php/pdo-query.md) podem ser executadas com uma configuração diferente para PDO:: sqlsrv_attr_direct_query.  
  
Se você usar [PDO](../../connect/php/pdo-prepare.md) e [Pdostatement](../../connect/php/pdostatement-execute.md) para executar uma consulta várias vezes usar parâmetros associados, a execução da instrução preparada otimiza a execução da consulta repetida.  Nessa situação, chame [PDO](../../connect/php/pdo-prepare.md) com PDO:: sqlsrv_attr_direct_query definido como False no parâmetro de matriz de opções de driver. Quando necessário, você pode executar instruções preparadas com PDO:: sqlsrv_attr_direct_query definido como False.  
  
Depois de chamar [PDO](../../connect/php/pdo-prepare.md), o valor de PDO:: sqlsrv_attr_direct_query não é possível alterar ao executar a consulta preparada.  
  
Se uma consulta exigir o contexto foi definido em uma consulta anterior, em seguida, execute as consultas com PDO:: sqlsrv_attr_direct_query definida como True. Por exemplo, se você usar tabelas temporárias em suas consultas, PDO:: sqlsrv_attr_direct_query deve ser definido como True.  
  
O exemplo a seguir mostra que, quando o contexto de uma instrução anterior é necessário, você precisa definir PDO:: sqlsrv_attr_direct_query como True.  Este exemplo usa as tabelas temporárias, que só estão disponíveis para instruções subsequentes no seu programa quando as consultas são executadas diretamente.  
  
```  
<?php  
   $conn = new PDO('sqlsrv:Server=(local)', '', '');  
   $conn->setAttribute(constant('PDO::SQLSRV_ATTR_DIRECT_QUERY'), true);  
  
   $stmt1 = $conn->query("DROP TABLE #php_test_table");  
  
   $stmt2 = $conn->query("CREATE TABLE #php_test_table ([c1_int] int, [c2_int] int)");  
  
   $v1 = 1;  
   $v2 = 2;  
  
   $stmt3 = $conn->prepare("INSERT INTO #php_test_table (c1_int, c2_int) VALUES (:var1, :var2)");  
  
   if ($stmt3) {  
      $stmt3->bindValue(1, $v1);  
      $stmt3->bindValue(2, $v2);  
  
      if ($stmt3->execute())  
         echo "Execution succeeded\n";       
      else  
         echo "Execution failed\n";  
   }  
   else  
      var_dump($conn->errorInfo());  
  
   $stmt4 = $conn->query("DROP TABLE #php_test_table");  
?>  
```  
  
## <a name="see-also"></a>Consulte também  
[Programação de guia para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
