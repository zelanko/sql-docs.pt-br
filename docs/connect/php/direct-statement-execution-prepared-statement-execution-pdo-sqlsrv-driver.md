---
title: Direcionar Statement - preparado instrução execução PDO_SQLSRV Driver | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c721a32936bf39d91042d6b7ac89a03a5fd85d6
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2018
ms.locfileid: "42785871"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdosqlsrv-driver"></a>Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico discute o uso do atributo PDO::SQLSRV_ATTR_DIRECT_QUERY para especificar a execução de instrução direta em vez do padrão, que é a execução da instrução preparada. Usar uma instrução preparada pode resultar em melhor desempenho se a instrução for executada mais de uma vez usando a associação de parâmetro.  
  
## <a name="remarks"></a>Remarks  
Se você quiser enviar uma [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução diretamente para o servidor sem preparação da instrução pelo driver, você pode definir o atributo PDO:: sqlsrv_attr_direct_query com [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) (ou como uma opção de driver passado para [PDO::__construct](../../connect/php/pdo-construct.md)) ou quando você chama [PDO:: Prepare](../../connect/php/pdo-prepare.md). Por padrão, o valor de PDO:: sqlsrv_attr_direct_query for False (use a execução da instrução preparada).  
  
Se você usar [PDO:: Query](../../connect/php/pdo-query.md), convém que a execução direta. Antes de chamar [PDO:: Query](../../connect/php/pdo-query.md), chame [PDO:: setAttribute](../../connect/php/pdo-setattribute.md) e defina o PDO:: sqlsrv_attr_direct_query como True.  Cada chamada para [PDO:: Query](../../connect/php/pdo-query.md) podem ser executadas com uma configuração diferente para PDO:: sqlsrv_attr_direct_query.  
  
Se você usar [PDO:: Prepare](../../connect/php/pdo-prepare.md) e [Pdostatement](../../connect/php/pdostatement-execute.md) para executar uma consulta várias vezes usar parâmetros associados, a execução da instrução preparada otimiza a execução da consulta repetida.  Nessa situação, chame [PDO:: Prepare](../../connect/php/pdo-prepare.md) com definido como False no parâmetro de matriz de opções de driver de PDO:: sqlsrv_attr_direct_query. Quando necessário, você pode executar instruções preparadas com PDO:: sqlsrv_attr_direct_query definido como False.  
  
Depois de chamar [PDO:: Prepare](../../connect/php/pdo-prepare.md), o valor de PDO:: sqlsrv_attr_direct_query não é possível alterar ao executar a consulta preparada.  
  
Se uma consulta exigir o contexto que foi definido em uma consulta anterior, em seguida, execute suas consultas com PDO:: sqlsrv_attr_direct_query definido como True. Por exemplo, se você usar tabelas temporárias em suas consultas, PDO:: sqlsrv_attr_direct_query deve ser definido como True.  
  
O exemplo a seguir mostra que, quando é necessário o contexto de uma instrução anterior, você precisa definir PDO:: sqlsrv_attr_direct_query como True.  Este exemplo usa as tabelas temporárias, que só estão disponíveis para instruções subsequentes no seu programa quando as consultas são executadas diretamente.  
  
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
  
## <a name="see-also"></a>Consulte Também  
[Guia de programação para os Drivers da Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
