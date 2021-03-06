---
title: SQL Server, objeto Erros de SQL | Microsoft Docs
description: Saiba mais sobre o objeto SQLServer:SQL Errors, que fornece contadores para monitorar Erros de SQL no SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Errors object
- SQLServer:SQL Errors
ms.assetid: 6e5273ca-29cb-4618-88a2-70b9b8d6cf76
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: e0433802954301c9ea5a9e483c0e54ca893f6b2d
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505568"
---
# <a name="sql-server-sql-errors-object"></a>SQL Server, objeto SQL Errors
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto **SQLServer:SQL Errors** no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar **Erros SQL**.  
  
 Esta tabela descreve os contadores **Erros de SQL** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contadores de Erros SQL do SQL Server|Descrição|  
|------------------------------------|-----------------|  
|**Erros/s**|Número de erros/segundo.|  
  
 Cada contador no objeto contém as seguintes instâncias:  
  
|Item|Definição|  
|----------|----------------|  
|**_Total**|Informações de todos os erros.|  
|**Erros de BD Offline**|Rastreia erros severos que fazem com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] torne offline o banco de dados atual.|  
|**Erros de Informação**|Informações referentes a mensagens de erro que fornecem informações a usuários, mas não causam erros.|  
|**Erros de Eliminação de Conexão**|Rastreia erros severos que fazem com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimine a conexão atual.|  
|**Erros de Usuário**|Informações sobre erros de usuário.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
