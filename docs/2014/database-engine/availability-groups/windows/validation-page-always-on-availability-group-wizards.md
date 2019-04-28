---
title: Página validação (assistentes de grupo de disponibilidade AlwaysOn) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.newagwizard.validation.f1
- sql12.swb.addreplicawizard.validation.f1
- sql12.swb.adddatabasewizard.validation.f1
helpviewer_keywords:
- ', listeners'
ms.assetid: c8971556-240c-491a-bc86-9cc72f71a3dd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6cf16c8afb363a1b7727b6da3a5f75bf966ab0d2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812980"
---
# <a name="validation-page-alwayson-availability-group-wizards"></a>Página de Validação (Assistentes de Grupo de Disponibilidade AlwaysOn)
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
|**Êxito**|Indica que a etapa de validação foi concluída com êxito|  
|**Aviso**|Indica um problema potencial com a configuração do grupo de disponibilidade.  Clique no link para exibir a mensagem de aviso.|  
  
 **Executar Novamente a Validação**  
 Clique para repetir as etapas da validação se você fizer uma alteração fora do assistente em resposta a um erro de validação.  
  

  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
 
  
## <a name="see-also"></a>Consulte também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
