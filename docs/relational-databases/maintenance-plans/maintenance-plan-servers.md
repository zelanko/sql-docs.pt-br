---
description: Plano de manutenção (Servidores)
title: Plano de manutenção (servidores) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.servers.f1
- sql13.swb.maint.maintplanproperties.server.f1
ms.assetid: ac24d1a8-dd2f-4162-b804-c0df1fc1e61d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1a991404f0acaba448958773f54a4836032ecd07
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88420850"
---
# <a name="maintenance-plan-servers"></a>Plano de manutenção (Servidores)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
   Use a caixa de diálogo **Servidores** para selecionar os servidores em que você quer executar o plano de manutenção.  
  
 É necessário configurar um ambiente multisservidor contendo um servidor mestre e um ou mais servidores de destino para criar um plano de manutenção multisservidor. Para planos de manutenção multisservidor, o servidor local deve ser configurado como um servidor mestre. Em ambientes multisservidor, essa caixa de diálogo exibe o servidor mestre **(local)** e todos os servidores de destino correspondentes. Um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é criado para o servidor local. Ele está habilitado ou desabilitado dependendo se o servidor **(local)** for selecionado. Se os servidores de destino estiverem selecionados, um trabalho multisservidor será criado e baixado para cada um dos servidores de destino selecionados. Se nenhum servidor de destino estiver selecionado, o trabalho multisservidor será excluído.  
  
## <a name="see-also"></a>Consulte Também  
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Criar um ambiente multisservidor](../../ssms/agent/create-a-multiserver-environment.md)   
 [Criar um servidor mestre](../../ssms/agent/make-a-master-server.md)   
 [Criar um servidor de destino](../../ssms/agent/make-a-target-server.md)  
  
  
