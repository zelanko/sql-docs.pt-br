---
title: Informações da publicação, Tokens de rastreamento (publicação transacional, SQL Server 2005 e versões posterior) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.tracertokens.f1
ms.assetid: a115ba95-17ae-45df-91bd-5a1a35f3745f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 287d565947a13621fd3ba39cff6437ff76894c03
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63021694"
---
# <a name="publication-information-tracer-tokens-transactional-publication-sql-server-2005-and-later"></a>Informações da Publicação, Tokens de Rastreamento (publicação transacional, SQL Server 2005 e versões posteriores)
  A guia **Tokens de Rastreamento** permite validar conexões e medir a latência de um sistema que usa replicação transacional. Um token (uma quantidade pequena de dados) é gravado no log de transações do banco de dados de publicação, marcado como se fosse uma transação replicada comum e enviado pelo sistema, permitindo um cálculo de:  
  
-   O tempo decorrido entre a confirmação de uma transação no Publicador e o comando correspondente inserido no banco de dados de distribuição no Distribuidor.  
  
-   O tempo decorrido entre um comando inserido no banco de dados de distribuição e a transação correspondente confirmada no Assinante.  
  
 Desses cálculos, você pode responder várias perguntas, enquanto incluindo:  
  
-   Quais Assinantes levam mais tempo para receber uma alteração do Publicador?  
  
-   Dos Assinantes esperados para receber o token de rastreamento quais, se houver, ainda não receberam?  
  
## <a name="options"></a>Opções  
 Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas**.  
  
-   **Escolher Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas**.  
  
-   **Filtrar**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro**.  
  
-   **Limpar Filtro**: Limpe todas as configurações de filtro para a grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Inserir Rastreador**  
 Clique para inserir um token de rastreamento no log de transações no Publicador.  
  
 **Hora de inserção**  
 Selecione uma hora, na qual um token de rastreamento foi inserido, para exibir informações de latência a partir daquela hora. Por padrão, informações da hora mais recente serão exibidas.  
  
> [!NOTE]  
>  Informações de token de rastreamento são retidas para o mesmo período de tempo que outros dados históricos, os quais são governados pelo período de retenção de histórico do banco de dados de distribuição. Para obter informações sobre como alterar as propriedades do banco de dados de distribuição, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](view-and-modify-distributor-and-publisher-properties.md).  
  
 **Assinatura**  
 O nome de cada assinatura na publicação.  
  
 **Publicador para Distribuidor**  
 O tempo decorrido entre a confirmação de uma transação no Publicador e o comando correspondente inserido no banco de dados de distribuição no Distribuidor. Um valor **Pendente** indica que o token ainda não alcançou o Distribuidor. Se o estado pendente persistir, verifique se o Log Reader Agent está em execução.  
  
 **Distribuidor para Assinante**  
 O tempo decorrido entre um comando inserido no banco de dados de distribuição e a transação correspondente confirmada no Assinante. Um valor **Pendente** indica que o token ainda não alcançou o Assinante. Se o estado pendente persistir, verifique se o Distribution Agent está em execução.  
  
 **Latência Total**  
 O tempo decorrido entre a confirmação de uma transação no Publicador e a confirmação da transação correspondente no Assinante. Isso representa a latência completa do sistema de replicação para esse Assinante neste momento. Um valor **Pendente** indica que o token ainda não alcançou o Assinante.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar e interromper um agente de replicação &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Medir a latência e validar as conexões para a replicação transacional](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [Monitorar o desempenho com o Replication Monitor](monitor/monitor-performance-with-replication-monitor.md)   
 [Monitorando a Replicação](monitoring-replication.md)   
 [Visão geral dos agentes de replicação](agents/replication-agents-overview.md)  
  
  
