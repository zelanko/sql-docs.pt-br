---
title: SQL Server, objeto Erros de SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
s.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Errors object
- SQLServer:SQL Errors
ms.assetid: 6e5273ca-29cb-4618-88a2-70b9b8d6cf76
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0372670c89a2367bf12bc646d6aada5ceba29776
ms.sourcegitcommit: ca038f1ef180e4e1b27910bbc5d87822cd1ed176
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52158584"
---
# <a name="sql-server-sql-errors-object"></a>SQL Server, objeto SQL Errors
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O objeto **SQLServer:SQL Errors** no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar **Erros SQL**.  
  
 Esta tabela descreve os contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Erros SQL** .  
  
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
  
  
