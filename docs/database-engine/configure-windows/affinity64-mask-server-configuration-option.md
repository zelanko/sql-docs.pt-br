---
title: Opção de configuração de servidor affinity64 mask | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- affinity64 mask option
- binding processors [SQL Server]
ms.assetid: 75ed08c7-f85c-4e15-9ee1-e7bc545d3293
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2888394a73e7ce56e55c867adb21a54d6be81cc3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68013172"
---
# <a name="affinity64-mask-server-configuration-option"></a>Opção affinity64 mask de configuração de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  A opção affinity64 mask associa processadores a threads específicos, de modo semelhante à opção affinity mask. Use a opção affinity mask para associar os primeiros 32 processadores e use affinity64 mask para associar os processadores restantes no computador. Esta opção é visível somente na versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] Em vez disso, use [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Opção affinity mask de configuração de servidor](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
