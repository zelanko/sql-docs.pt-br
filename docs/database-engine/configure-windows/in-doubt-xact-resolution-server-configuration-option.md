---
title: "Opção de configuração de servidor in-doubt xact resolution | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- distributed transactions [SQL Server], unresolved transactions
- unresolved transactions
- in-doubt xact resolution option
ms.assetid: 3426fd32-cad2-4f2f-8ca9-e0296cc12703
caps.latest.revision: "25"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fce09d60d98c094e3b47440fb900ec7d6523daa6
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="in-doubt-xact-resolution-server-configuration-option"></a>Opção de configuração de servidor in-doubt xact resolution
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a opção **in-doubt xact resolution** para controlar o resultado padrão de transações que o MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ) não pode resolver. A incapacidade de resolver transações pode estar relacionada ao tempo de desligamento do MS DTC ou a um resultado de transação desconhecido no momento da recuperação.  
  
 A tabela seguinte lista os possíveis valores de resultado para resolver uma transação incerta.  
  
|Valor de resultado|Description|  
|-------------------|-----------------|  
|0|Nenhuma suposição. Recuperação falhará se o MS DTC não puder resolver nenhuma transação incerta.|  
|1|Suponha confirmação. Supõe-se que qualquer transação incerta de MS DTC esteja confirmada.|  
|2|Suponha anulação. Supõe-se que quaisquer transações incertas de MS DTC tenham sido anuladas.|  
  
 Para minimizar a possibilidade de tempo de inatividade estendido, um administrador pode configurar essa opção para supor confirmação ou anulação, como mostrado no exemplo seguinte.  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 2 -– presume abort  
GO  
RECONFIGURE  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 Como alternativa, o administrador pode deixar o padrão (nenhuma suposição) e permitir a falha da recuperação para ser alertado sobre uma falha de DTC, como mostrado no exemplo seguinte.  
  
```  
sp_configure 'show advanced options', 1  
GO  
RECONFIGURE  
GO  
sp_configure 'in-doubt xact resolution', 1 -– presume commit  
GO  
reconfigure  
GO  
ALTER DATABASE pubs SET ONLINE –- run recovery again  
GO  
sp_configure 'in-doubt xact resolution', 0 –- back to no assumptions  
GO  
sp_configure 'show advanced options', 0  
GO  
RECONFIGURE  
GO  
  
```  
  
 A opção **in-doubt xact resolution** é uma opção avançada. Se estiver usando o procedimento armazenado no sistema **sp_configure** para alterar a configuração, é possível alterar o **in-doubt xact resolution** apenas quando **mostrar opções avançadas** estiver definida como 1. A configuração entra em vigor imediatamente sem a reinicialização do servidor.  
  
> [!NOTE]  
>  A configuração consistente desta opção por todas as instâncias [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envolvidas em qualquer transação distribuída ajudará a evitar inconsistências de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
