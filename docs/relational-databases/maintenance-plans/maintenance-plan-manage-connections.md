---
title: Plano de manutenção (Gerenciar conexões) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: maintenance-plans
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.swb.maint.connections.f1
ms.assetid: 95ad9375-6584-423e-b9de-0e86782f8017
caps.latest.revision: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f7a35cc6e39beb2e81b092d862b881e4922c491
ms.sourcegitcommit: 6e16d1616985d65484c72f5e0f34fb2973f828f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/16/2018
---
# <a name="maintenance-plan-manage-connections"></a>Plano de manutenção (Gerenciar Conexões)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use a caixa de diálogo **Gerenciar Conexões** para especificar as propriedades das conexões usadas por planos de manutenção. Quando você cria um plano de manutenção, é criada uma conexão local para o servidor em que você criou o plano. Use essa conexão para criar tarefas que executam trabalho nessa conexão local. Quando necessário, use a caixa de diálogo **Gerenciar Conexões** para adicioná-las. Quando conexões adicionais são configuradas, elas aparecem na caixa de conexões para cada tarefa.  
  
## <a name="options"></a>Opções  
 **Servidor**  
 Instância de servidor.  
  
 **Autenticação**  
 Indica se a conexão é feita com autenticação do Windows ou com autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

> [!IMPORTANT]  
> O pacote é armazenado no banco de dados **msdb** com seu **ProtectionLevel** definida como **ServerStorage**, portanto, quando a *Autenticação do SQL Server* é usada, a senha não será criptografada no **msdb**. Você pode usar a *Autenticação do SQL Server* desde que **msdb** esteja protegido, porém é recomendado usar a *Autenticação do Windows*

## <a name="see-also"></a>Consulte Também  
 [Planos de Manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
  
