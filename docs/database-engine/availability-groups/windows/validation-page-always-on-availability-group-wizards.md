---
title: "Página Validação (Assistentes do Grupo de Disponibilidade AlwaysOn) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.addreplicawizard.validation.f1
- sql13.swb.adddatabasewizard.validation.f1
- sql13.swb.newagwizard.validation.f1
helpviewer_keywords:
- ', listeners'
ms.assetid: c8971556-240c-491a-bc86-9cc72f71a3dd
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6f8c43c0c8a698fb38f67f7ba6ba0ad897692f00
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="validation-page-always-on-availability-group-wizards"></a>Página Validação (Assistentes do Grupo de Disponibilidade AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  
    
  Este tópico da ajuda descreve as opções da página **Validação** . Este tópico aplica-se ao [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)], ao [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]e ao [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Use esta página para validar se o ambiente dá suporte a todas as opções de configuração feitas nas páginas anteriores do assistente.  
  
##  <a name="PageOptions"></a> Opções da página Validação  
 **Resultados da validação de grupo de disponibilidade.**  
 Esta grade exibe os resultados de cada etapa de validação concluída. As colunas da grade são as seguintes:  
  
 **Nome**  
 Exibe uma frase que descreve uma etapa específica.  
  
 **Resultado**  
 Exibe um dos seguintes textos de hiperlink. Para obter mais informações sobre o resultado de determinada etapa de validação, clique no hiperlink.  
  
|Resultado|Descrição|  
|------------|-----------------|  
|**Erro**|Indica se houve falha na etapa de validação. Clique no link para exibir a mensagem de erro.|  
|**Ignorado**|Indica que a etapa de validação foi ignorada porque não é necessária por suas seleções. Clique no link para exibir o motivo pelo qual uma etapa foi ignorada.|  
|**Success**|Indica que a etapa de validação foi concluída com êxito|  
|**Aviso**|Indica um problema potencial com a configuração do grupo de disponibilidade.  Clique no link para exibir a mensagem de aviso.|  
  
 **Executar Novamente a Validação**  
 Clique para repetir as etapas da validação se você fizer uma alteração fora do assistente em resposta a um erro de validação.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  

