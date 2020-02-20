---
title: Instrução direta – execução de instrução preparada no driver PDO_SQLSRV | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 05544ca6-1e07-486c-bf03-e8c2c25b3024
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa9e544fb7b79009d86a5742946a722d5adc18f2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "67993624"
---
# <a name="direct-statement-execution-and-prepared-statement-execution-in-the-pdo_sqlsrv-driver"></a>Execução de instrução direta e execução de instrução preparada no driver PDO_SQLSRV
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Este tópico discute o uso do atributo PDO::SQLSRV_ATTR_DIRECT_QUERY para especificar a execução de instrução direta em vez do padrão, que é a execução da instrução preparada. Usar uma instrução preparada pode resultar em melhor desempenho se a instrução for executada mais de uma vez usando a associação de parâmetros.  
  
## <a name="remarks"></a>Comentários  
Se você quiser enviar uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] diretamente para o servidor sem a preparação da instrução pelo driver, poderá definir o atributo PDO::SQLSRV_ATTR_DIRECT_QUERY com [PDO::setAttribute](../../connect/php/pdo-setattribute.md) (ou como uma opção de driver passada para [PDO::__construct](../../connect/php/pdo-construct.md)) ou quando você chamar [PDO::prepare](../../connect/php/pdo-prepare.md). Por padrão, o valor de PDO::SQLSRV_ATTR_DIRECT_QUERY é false (use a execução de instrução preparada).  
  
Se você usar [PDO::query](../../connect/php/pdo-query.md), talvez seja melhor que você use a execução direta. Antes de chamar [PDO::query](../../connect/php/pdo-query.md), chame [PDO::setAttribute](../../connect/php/pdo-setattribute.md) e defina PDO::SQLSRV_ATTR_DIRECT_QUERY como true.  Cada chamada para [PDO::query](../../connect/php/pdo-query.md) pode ser executada com uma configuração diferente para PDO::SQLSRV_ATTR_DIRECT_QUERY.  
  
Se você usar [PDO::prepare](../../connect/php/pdo-prepare.md) e [PDOStatement::execute](../../connect/php/pdostatement-execute.md) para executar uma consulta várias vezes usando parâmetros associados, a execução da instrução preparada otimizará a execução da consulta repetida.  Nessa situação, chame [PDO::prepare](../../connect/php/pdo-prepare.md) com PDO::SQLSRV_ATTR_DIRECT_QUERY definido como False no parâmetro de matriz de opções de driver. Quando necessário, você pode executar instruções preparadas com PDO::SQLSRV_ATTR_DIRECT_QUERY definido como False.  
  
Depois de chamar [PDO::prepare](../../connect/php/pdo-prepare.md), o valor de PDO::SQLSRV_ATTR_DIRECT_QUERY não pode ser alterado ao executar a consulta preparada.  
  
Se uma consulta exigir o contexto que foi definido em uma consulta anterior, execute suas consultas com PDO::SQLSRV_ATTR_DIRECT_QUERY definido como True. Por exemplo, se você usar tabelas temporárias em suas consultas, PDO::SQLSRV_ATTR_DIRECT_QUERY precisará ser definido como true.  
  
O exemplo a seguir mostra que, quando o contexto de uma instrução anterior é necessário, você precisa definir PDO::SQLSRV_ATTR_DIRECT_QUERY como true. Este exemplo usa tabelas temporárias, que só estão disponíveis para instruções subsequentes em seu programa quando as consultas são executadas diretamente.  
  
> [!NOTE]
> Se a consulta for para invocar um procedimento armazenado e tabelas temporárias forem usadas neste procedimento armazenado, use [PDO::exec](../../connect/php/pdo-exec.md) em vez disso.

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
[Guia de programação do Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
