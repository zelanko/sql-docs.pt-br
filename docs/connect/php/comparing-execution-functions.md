---
title: Como comparar funções de execução
description: Este tópico lista as diferentes funções de execução de consulta ao usar os Drivers da Microsoft para PHP para SQL Server
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- executing queries
ms.assetid: 130fc0fd-87dd-46b2-918f-de9dc572c769
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 33d7ebe420dd59d4f659dbe2ce6c784b49b89d04
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680741"
---
# <a name="comparing-execution-functions"></a>Comparando funções de execução
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Os [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] fornecem várias opções para a execução de funções.  

## <a name="sqlsrv-execution-functions"></a>Funções de execução do SQLSRV  
Se estiver usando o driver SQLSRV, use [sqlsrv_query](../../connect/php/sqlsrv-query.md) para executar uma única consulta e [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md) com [sqlsrv_execute](../../connect/php/sqlsrv-execute.md) para executar uma instrução preparada várias vezes com valores de parâmetros diferentes para cada execução.  

## <a name="pdo_sqlsrv-execution-functions"></a>Funções de execução do PDO_SQLSRV 
Se estiver usando o driver PDO_SQLSRV, é possível executar uma consulta com um destes comandos:  
  
-   [PDO::exec](../../connect/php/pdo-exec.md)  
  
-   [PDO::query](../../connect/php/pdo-query.md)  
  
-   [PDO::prepare](../../connect/php/pdo-prepare.md) e [PDOStatement::execute](../../connect/php/pdostatement-execute.md).  
  
## <a name="see-also"></a>Consulte Também  
[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Referência do driver PDO_SQLSRV](../../connect/php/pdo-sqlsrv-driver-reference.md)

[Guia de programação do Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)
  
