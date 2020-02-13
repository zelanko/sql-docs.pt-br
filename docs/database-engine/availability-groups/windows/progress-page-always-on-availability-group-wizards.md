---
title: Página Progresso (Assistentes do Grupo de Disponibilidade AlwaysOn)
description: Uma descrição das opções encontradas na 'Página Progresso' do Assistente do Grupo de Disponibilidade AlwaysOn no SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.failoverwizard.progress.f1
- sql13.swb.adddatabasewizard.progress.f1
- sql13.swb.addreplicawizard.progress.f1
- sql13.swb.newagwizard.progress.f1
ms.assetid: bd3b0306-8384-4120-a1c9-03825f0ae26a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 87201ed5c3d2368f54e2ffb0c57391322066a30b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68014483"
---
# <a name="progress-page-always-on-availability-group-wizards"></a>Página Progresso (Assistentes do Grupo de Disponibilidade AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use esta caixa de diálogo para exibir o progresso de um assistente do [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] que você está executando no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. A barra de progresso indica o progresso relativo das etapas que o assistente está executando.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Mais detalhes**  
 Clique na seta para baixo para exibir uma grade de progresso que lista todas as etapas concluídas, em ordem, seguidas pela operação em andamento no momento. A grade contém as seguintes colunas:  
  
 **Nome**  
 Exibe uma frase que descreve uma etapa específica.  
  
 **Status**  
 Indica o resultado das etapas concluídas e o percentual de conclusão da etapa atual, da seguinte maneira:  
  
|Result|Descrição|  
|------------|-----------------|  
|**Erro**|Indica que a operação desta etapa experimentou um erro. Clique no link para exibir uma caixa de diálogo de mensagem que descreve o erro.|  
|**Em andamento (** *percentual concluído* **)**|Indica que a operação está ocorrendo agora e estima o percentual desta etapa que foi concluída.|  
|**Êxito**|Indica que a operação desta etapa foi concluída com êxito.|  
  
 **Menos Detalhes**  
 Clique para ocultar a grade de progresso.  
  
 **Cancelar**  
 Clique para ignorar todas as operações restantes e sair do assistente.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
-   [Usar o Assistente de Grupo de Disponibilidade de Failover &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
