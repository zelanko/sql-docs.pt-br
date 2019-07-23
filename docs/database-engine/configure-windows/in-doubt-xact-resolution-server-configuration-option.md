---
title: Opção de configuração de servidor in-doubt xact resolution | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- distributed transactions [SQL Server], unresolved transactions
- unresolved transactions
- in-doubt xact resolution option
ms.assetid: 3426fd32-cad2-4f2f-8ca9-e0296cc12703
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 6bfdee182770e24896796bc3837d5c17d3d73da9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67998051"
---
# <a name="in-doubt-xact-resolution-server-configuration-option"></a>Opção de configuração de servidor in-doubt xact resolution
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a opção **in-doubt xact resolution** para controlar o resultado padrão de transações que o MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ) não pode resolver. A incapacidade de resolver transações pode estar relacionada ao tempo de desligamento do MS DTC ou a um resultado de transação desconhecido no momento da recuperação.  
  
 A tabela seguinte lista os possíveis valores de resultado para resolver uma transação incerta.  
  
|Valor de resultado|Descrição|  
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
sp_configure 'in-doubt xact resolution', 2 -- presume abort  
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
sp_configure 'in-doubt xact resolution', 1 -- presume commit  
GO  
reconfigure  
GO  
ALTER DATABASE pubs SET ONLINE -- run recovery again  
GO  
sp_configure 'in-doubt xact resolution', 0 -- back to no assumptions  
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
  
  
