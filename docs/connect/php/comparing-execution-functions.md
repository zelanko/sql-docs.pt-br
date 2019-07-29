---
title: Comparando funções de execução | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2b4d6c85c399589aae4eedbaade4bbdc4f70609
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993745"
---
# <a name="comparing-execution-functions"></a>Comparando funções de execução
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] fornecem várias opções para a execução de funções.  

## <a name="sqlsrv-execution-functions"></a>Funções de execução SQLSRV  
Se estiver usando o driver SQLSRV, use [sqlsrv_query](../../connect/php/sqlsrv-query.md) para executar uma única consulta e [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) com [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) para executar uma instrução preparada várias vezes com valores de parâmetros diferentes para cada execução.  

## <a name="pdosqlsrv-execution-functions"></a>Funções de execução PDO_SQLSRV 
Se estiver usando o driver PDO_SQLSRV, é possível executar uma consulta com um destes comandos:  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) e [PDOStatement::execute](../../connect/php/pdostatement-execute.md).  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[PDO_SQLSRV Driver Reference](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Guia de programação para o Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
