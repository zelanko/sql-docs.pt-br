---
title: Opção de configuração de servidor affinity64 Input-Output mask | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- binding processors [SQL Server]
- affinity64 I/O mask option
ms.assetid: d304eae7-5116-40ee-a0fa-0a3c0bc20c01
caps.latest.revision: 17
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4ffa722e06e148cc6d18835409644c442c854e5f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37185234"
---
# <a name="affinity64-input-output-mask-server-configuration-option"></a>Opção de configuração do servidor affinity64 I/O mask
  A **affinity64 I/O mask** associa a E/S de disco do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a um subconjunto especificado de CPUs, de forma semelhante à opção **affinity I/O mask** . Use **affinity I/O mask** para associar os primeiros 32 processadores e use **affinity64 I/O mask** para associar os processadores restantes no computador. Se você reconfigurar a **affinity64 I/O mask**, será necessário reinicializar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta opção é visível somente na versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Opção de configuração do servidor de máscara de Entrada-Saída de afinidade](affinity-input-output-mask-server-configuration-option.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
