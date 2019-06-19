---
title: Opção de configuração de servidor affinity64 Input-Output mask | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- binding processors [SQL Server]
- affinity64 I/O mask option
ms.assetid: d304eae7-5116-40ee-a0fa-0a3c0bc20c01
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: c30943344025d9b163c8d96909d4b01ad63b13a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66786931"
---
# <a name="affinity64-input-output-mask-server-configuration-option"></a>Opção de configuração do servidor affinity64 I/O mask
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  A **affinity64 I/O mask** associa a E/S de disco do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a um subconjunto especificado de CPUs, de forma semelhante à opção **affinity I/O mask** . Use **affinity I/O mask** para associar os primeiros 32 processadores e use **affinity64 I/O mask** para associar os processadores restantes no computador. Se você reconfigurar a **affinity64 I/O mask**, será necessário reinicializar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta opção é visível somente na versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Opção de configuração do servidor de máscara de Entrada-Saída de afinidade](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
