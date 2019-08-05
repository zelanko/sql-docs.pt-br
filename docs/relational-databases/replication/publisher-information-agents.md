---
title: Informações sobre o Publicador, agentes | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publisherinfo.commonjobs.f1
ms.assetid: 2346c00d-c269-45a1-af14-68e7fd7ebd7e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: b006eac4981866bbadadaf47bc6d895e3abd0f9e
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68769729"
---
# <a name="publisher-information-agents"></a>Informações do Publicador, Agentes
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  A guia **Agentes** exibe informações sobre os agentes e trabalhos de manutenção associados ao Publicador:  
  
-   Snapshot Agent que é exibido para todas as publicações.  
  
-   Log Reader Agent que é exibido para todas as publicações transacionais.  
  
-   Queue Reader Agent que é exibido para publicações transacionais habilitadas para assinaturas de atualização enfileiradas.  
  
-   Trabalhos de manutenção exibidos para todas as publicações:  
  
    -   Assinaturas de reinicialização, com falhas de validação de dados  
  
    -   Limpeza do histórico de agente: distribuição  
  
    -   Atualizador de monitoração de replicação para distribuição  
  
    -   Verificação de agentes de replicação  
  
    -   Limpeza de distribuição: distribuição  
  
    -   Limpeza de assinatura expirada  
  
 Para obter mais informações sobre esses trabalhos, consulte [Administração do agente de replicação](../../relational-databases/replication/agents/replication-agent-administration.md).  
  
## <a name="options"></a>Opções  
 Para exibir informações sobre um agente ou trabalho, selecione no menu suspenso **Tipos de Agente e Trabalho** . Para obter informações mais detalhadas e tarefas relacionadas a um agente ou trabalho, clique com o botão direito na linha do agente ou trabalho e clique em uma opção no menu de atalho. Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas**.  
  
-   **Escolher Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas**.  
  
-   **Filtrar**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro**.  
  
-   **Limpar Filtro**: Limpe todas as configurações de filtro para a grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 As seções a seguir descrevem os dados exibidos nesta guia para cada agente ou trabalho.  
  
### <a name="snapshot-agent"></a>Snapshot Agent  
 **Status**  
 O status do agente. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Repetir  
  
-   Executando  
  
-   Concluído  
  
 **Publicação**  
 O nome da publicação com a qual o agente está associado.  
  
 **Última Hora de Início**  
 A última hora de início do agente.  
  
 **Duration**  
 O tempo de execução do agente. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
 **Taxa de Entrega**  
 A taxa, em comandos por segundo, com a qual os comandos de inicialização são confirmados no banco de dados de distribuição durante a execução mais recente do agente.  
  
 **#Trans**  
 O número de transações confirmado no banco de dados de distribuição durante a execução mais recente do agente.  
  
 **#Cmds**  
 O número de comandos confirmado no banco de dados de distribuição durante a execução mais recente do agente. Um comando é equivalente a uma alteração de dados, como uma atualização.  
  
### <a name="log-reader-agent"></a>Agente de Leitor de Log  
 **Status**  
 O status do agente. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Repetir  
  
-   Executando  
  
-   Não está sendo executado  
  
 **Banco de dados de publicação**  
 O nome da publicação com a qual o agente está associado.  
  
 **Última Hora de Início**  
 A última hora de início do agente.  
  
 **Duration**  
 O tempo de execução do agente. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
 **Taxa de Entrega**  
 A taxa, em comandos por segundo, com a qual as alterações são confirmadas no banco de dados de distribuição.  
  
 **Latência**  
 É o período de tempo, em segundos, decorrido entre a confirmação da alteração mais recente no banco de dados de publicação e a confirmação do comando correspondente no banco de dados de distribuição.  
  
 **#Trans**  
 O número de transações confirmado no banco de dados de distribuição durante a execução mais recente do agente.  
  
 **#Cmds**  
 O número de comandos confirmado no banco de dados de distribuição durante a execução mais recente do agente. Um comando é equivalente a uma alteração de dados, como uma atualização.  
  
 **Avg. #Cmds**  
 O número médio de comandos por transação durante a execução mais recente do agente.  
  
### <a name="queue-reader-agent"></a>Queue Reader Agent  
 **Status**  
 O status do agente. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Repetir  
  
-   Executando  
  
-   Não está sendo executado  
  
 **Banco de dados de distribuição**  
 O nome do banco de dados de distribuição ao qual o agente está associado.  
  
 **Última Hora de Início**  
 A última hora de início do agente.  
  
 **Duration**  
 O tempo de execução do agente. O tempo representa o tempo decorrido, se o agente estiver sendo executado no momento, e o tempo total, se o agente foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do agente.  
  
 **Taxa de Entrega**  
 A taxa, em comandos por segundo, com a qual as alterações são confirmadas no banco de dados de distribuição.  
  
 **Latência**  
 É o período de tempo, em segundos, decorrido entre confirmação da alteração mais recente no banco de dados de assinatura e a confirmação do comando correspondente no banco de dados de publicação.  
  
 **#Trans**  
 O número de transações confirmado no banco de dados de publicação durante a execução mais recente do agente.  
  
 **#Cmds**  
 O número de comandos confirmados no banco de dados de publicação durante a execução mais recente do agente. Um comando é equivalente a uma alteração de dados, como uma atualização.  
  
 **Avg. #Cmds**  
 O número médio de comandos por transação durante a execução mais recente do agente.  
  
### <a name="maintenance-jobs"></a>Trabalhos de manutenção  
 **Status**  
 O status de cada trabalho. A seguinte lista mostra os possíveis valores de status:  
  
-   Erro  
  
-   Repetir  
  
-   Executando  
  
-   Não está sendo executado  
  
 **Trabalho**  
 O nome do trabalho.  
  
 **Última Hora de Início**  
 A última hora de início do trabalho.  
  
 **Duration**  
 O tempo de execução do trabalho. O tempo representa o tempo decorrido, se o trabalho estiver sendo executado no momento, e o tempo total, se o trabalho foi executado anteriormente.  
  
 **Última Ação**  
 A última ação executada durante a execução mais recente do trabalho.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar o Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas usando o Replication Monitor](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitorando a Replicação](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
