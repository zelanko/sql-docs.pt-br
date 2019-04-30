---
title: Informações do publicador, inspeção de assinatura (publicação de mesclagem, SQL Server 2005 e versões posterior) da lista | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publisherinfo.subscriptionssummary.merge.f1
ms.assetid: 4ec956bf-5cef-4377-a1d1-8c7f0107a6cb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2fcff4e55ca4a2935f90b360965a1bc5fefe5656
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63261796"
---
# <a name="publisher-information-subscription-watch-list-merge-publication-sql-server-2005-and-later"></a>Informações do Publicador, Lista de Observação da Assinatura (publicação de mesclagem, SQL Server 2005 e versões posteriores)
  A guia **Lista de Observação da Assinatura** está disponível para os Distribuidores que executam o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores; seu propósito é exibir informações sobre assinaturas de todas as publicações disponíveis no Publicador selecionado. Você pode filtrar a lista de assinaturas para ver erros, avisos e qualquer assinatura de desempenho insatisfatório. Essa guia fornece uma localização única para o administrador monitorar todas as atividades de replicação em um Publicador: O Replication Monitor exibe todas as assinaturas que exigem atenção com base no tipo de replicação selecionado e na opção escolhida na caixa de listagem suspensa **Mostrar**. Como os itens mostrados nessa guia são baseados no status atual e no desempenho, as assinaturas serão exibidas nessa página somente se corresponderem à opção da caixa de listagem **Mostrar** naquele momento.  
  
## <a name="options"></a>Opções  
 Para obter informações mais detalhadas e tarefas relacionadas a uma assinatura, clique com o botão direito do mouse na linha dessa assinatura e clique em uma opção no menu de atalho. Para alterar a forma como a grade exibe os dados, clique com o botão direito do mouse na grade e clique em uma destas opções:  
  
-   **Classificar**: classifique uma ou mais colunas na caixa de diálogo **Classificar Colunas**.  
  
-   **Escolher Colunas para Mostrar**: selecione quais colunas devem ser exibidas e a ordem em que devem ser exibidas, na caixa de diálogo **Selecionar Colunas**.  
  
-   **Filtrar**: filtre linhas na grade com base em valores de colunas da caixa de diálogo **Configurações de Filtro**.  
  
-   **Limpar Filtro**: Limpe todas as configurações de filtro para a grade.  
  
 As configurações de filtro são específicas de cada grade. A seleção e a classificação da coluna são aplicadas a todas as grades do mesmo tipo, como a grade de publicações de cada Publicador.  
  
 **Mostrar Assinaturas Mescladas**  
 Selecione o tipo de assinatura (transacional, instantâneo ou mesclagem) a ser exibida para o Publicador selecionado.  
  
 **Mostrar**  
 Selecione os estados de assinatura a serem exibidos para o tipo de assinatura selecionado. Por exemplo, você pode optar por exibir somente as assinaturas que tiverem um erro.  
  
 **Status**  
 O status de cada assinatura que é determinado pelo status do Merge Agent.  
  
 Por padrão, a grade que contém informações de assinatura é classificada pela coluna **Status** (e depois pela coluna **Desempenho** para assinaturas com o mesmo status). A lista a seguir mostra os valores de status possíveis e a ordem de classificação dos valores (por exemplo, os erros são sempre mostrados na parte superior da grade).  
  
-   Erro  
  
-   Desempenho crítico  
  
-   Mesclagem de execução longa  
  
-   Expirando em breve/Expirado  
  
-   Assinatura não inicializada  
  
-   Tentando novamente comando com falha  
  
-   Sincronizando  
  
-   Não sincronizando  
  
 A ordem de classificação também determina qual valor será exibido se uma determinada assinatura estiver em mais de um estado. Por exemplo, se uma assinatura tiver um erro e expirar em breve, a coluna **Status** exibirá **Erro**.  
  
 Os valores de status **Desempenho crítico**, **Mesclagem de execução longa**, **Expirando em breve/Expirado**e **Assinatura não inicializada** são avisos. Quando um aviso é exibido, a coluna **Status** também exibe se um agente está sincronizando. Por exemplo, o status poderia ser **Sincronizando, Desempenho Crítico**.  
  
 Os valores de status **Expirando em breve/Expirado** e **Mesclagem de Execução Longa** só poderão ser exibidos se os limites forem definidos. O valor de status **Desempenho crítico** só pode ser exibido depois de cinco sincronizações de assinatura com o mesmo tipo de conexão (discada ou LAN). Para obter informações sobre medidas de desempenho e definir limites, consulte [Monitor Performance with Replication Monitor](monitor/monitor-performance-with-replication-monitor.md) (Monitorar o desempenho com o Replication Monitor) e [Set Thresholds and Warnings in Replication Monitor](monitor/set-thresholds-and-warnings-in-replication-monitor.md) (Definir limites e avisos no Replication Monitor).  
  
 **Assinatura**  
 O nome de cada assinatura no formato:*SubscriberName: SubscriptionDatabaseName*.  
  
 **Nome amigável**  
 A descrição de cada assinatura. A descrição é inserida na caixa de diálogo **Propriedades da assinatura** ou especificada com o parâmetro **@description** de [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql) ou [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Os usuários geralmente usam a descrição como um "nome amigável" ou apelido para a assinatura.  
  
 **Publicação**  
 O nome da publicação com a qual uma assinatura é sincronizada, no formato: *PublicationDatabaseName: PublicationName*.  
  
 **Desempenho**  
 A classificação de desempenho de cada assinatura, com base nas medidas mais recentes de taxa de entrega calculadas pelo Replication Monitor. A classificação é determinada comparando o desempenho de uma assinatura individual com o desempenho histórico médio de assinaturas com a publicação que tem o mesmo tipo de conexão (discada ou LAN). O Replication Monitor exibe um valor após a ocorrência de cinco sincronizações com 50 ou mais alterações cada, no mesmo tipo de conexão. Se houver menos de cinco sincronizações com 50 ou mais alterações ou se a sincronização mais recente tiver menos de 50 alterações, essa coluna ficará em branco.  
  
> [!NOTE]  
>  O desempenho é baseado no tipo de conexão exibido na coluna **Conexão** ; portanto, é possível que uma assinatura com uma taxa de entrega mais baixa exiba uma classificação de desempenho melhor do que outra assinatura, se a primeira assinatura estiver sincronizada em uma conexão mais lenta.  
  
 A classificação de desempenho é um dos seguintes valores:  
  
-   Excelente  
  
-   Bom  
  
-   Razoável  
  
-   Fraco  
  
 Para obter mais informações sobre como as classificações de desempenho são definidas e como os limites de desempenho são configurados, consulte [Monitorar o desempenho com o Replication Monitor](monitor/monitor-performance-with-replication-monitor.md).  
  
 **Taxa de Entrega**  
 O número de linhas por segundo processado pelo Merge Agent.  
  
 **Última Sincronização**  
 A hora da última execução do Merge Agent. As alterações podem ou não ter sido processadas durante essa sincronização. Se a sincronização estiver em progresso, um valor da porcentagem concluída será exibido.  
  
 **Duration**  
 A quantidade de tempo de execução do Merge Agent durante a última sincronização. O tempo representa o tempo decorrido, se o Merge Agent estiver sendo executado no momento, e o tempo total, se o Merge Agent foi sincronizado anteriormente.  
  
 **Conexão**  
 O tipo de conexão entre o Assinante e o Editor. Os valores possíveis são **LAN**, **Discada**e **Internet**. O valor **Internet** será exibido se a assinatura usar sincronização da Web.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciar o Replication Monitor](monitor/start-the-replication-monitor.md)   
 [Exibir informações e executar tarefas usando o Replication Monitor](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitorando a Replicação](monitoring-replication.md)   
 [Sincronização da Web para replicação de mesclagem](web-synchronization-for-merge-replication.md)  
  
  
