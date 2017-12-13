---
title: Validar dados no assinante | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Subscribers [SQL Server replication], data validation
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication], SQL Server Management Studio
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d78ec0ec5dcbb0fa259cc26950a9de9742bfaa6c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="validate-data-at-the-subscriber"></a>Validar dados no assinante
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Este tópico descreve como validar os dados no Assinante no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)] ou RMO (Replication Management Objects).  
  
 A validação de dados é um processo de três etapas:  
  
1.  Uma única assinatura ou todas as assinaturas para uma publicação são *marcadas* para validação. Marque as assinaturas para validação nas caixas de diálogo **Validar Assinatura**, **Validar Assinaturas**e **Validar Todas as Assinaturas** que estão disponíveis na pasta **Publicações Locais** e na pasta **Assinaturas Locais** no [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você também pode marcar assinaturas da guia **Todas as Assinaturas** , a guia **Lista de Observação da Assinatura** e o nó de publicações no Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../../relational-databases/replication/monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor).  
  
2.  Uma assinatura é validada da próxima vez em que for sincronizada pelo Distribution Agent (para replicação transacional) ou pelo Merge Agent (replicação de mesclagem). O Distribution Agent normalmente é executado continuamente, nesse caso a validação ocorre imediatamente; o Merge Agent normalmente é executado por solicitação, neste caso a validação ocorrerá após você executar o agente.  
  
3.  Exibir os resultados de validação:  
  
    -   Nas janelas de detalhes do Replication Monitor: na guia **Histórico do Distribuidor para o Assinante** para replicação transacional e na guia **Histórico de Sincronização** para replicação de mesclagem.  
  
    -   Na caixa de diálogo **Exibir Status de Sincronização** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para validar dados no Assinante, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Os procedimentos para o Replication Monitor são somente para assinaturas push porque as assinaturas pull não podem ser sincronizadas no Replication Monitor. Porém, você pode marcar uma assinatura para validação e exibir os resultados da validação para assinaturas pull no Replication Monitor.  
  
-   Os resultados da validação indicam se a validação obteve êxito ou se falhou, porém não especifica quais linhas falharam a validação caso tenha ocorrido uma falha. Para comparar dados no Publicador e no Assinante, use o [tablediff Utility](../../tools/tablediff-utility.md). Para obter informações sobre como usar esse utilitário com os dados replicados, consulte [Comparar diferenças em tabelas replicadas &#40;programação de replicação&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-validate-data-for-subscriptions-to-a-transactional-publication-management-studio"></a>Para validar dados para assinaturas para uma publicação transacional (Management Studio)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse na publicação para a qual você quer validar assinaturas e então clique em **Validar Assinaturas**.  
  
4.  Na caixa de diálogo **Validar Assinaturas** , selecione quais assinatura validar:  
  
    -   Selecione **Validar todas as assinaturas SQL Server**  
  
    -   Selecione **Validar estas assinaturas**e então selecione uma ou mais assinaturas.  
  
5.  Para especificar o tipo de validação a ser executado (contagem de linha ou contagem de linha e soma de verificação) clique em **Opções de Validação**e então especifique as opções na caixa de diálogo **Opções de Validação de Assinatura** .  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Exiba os resultados da validação no Replication Monitor ou a caixa de diálogo **Exibir Status da Sincronização** . Para cada assinatura:  
  
    1.  Expanda a publicação, clique com o botão direito do mouse na assinatura e então clique em **Exibir Status da Sincronização**.  
  
    2.  Se o agente não estiver sendo executado clique em **Iniciar** na caixa de diálogo **Exibir Status da Sincronização** . A caixa de diálogo exibirá mensagens informativas relacionadas à validação.  
  
     Se você não vir nenhuma mensagem relacionada à validação, o agente já registrou uma mensagem subsequente. Neste caso, exiba os resultados de validação no Replication Monitor. Para obter mais informações, consulte os procedimentos de instruções do Replication Monitor neste tópico.  
  
#### <a name="to-validate-data-for-a-single-subscription-to-a-merge-publication-management-studio"></a>Para validar dados para uma única assinatura para uma publicação de mesclagem (Management Studio)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Expanda a publicação para a qual você quer validar assinaturas, clique com o botão direito do mouse na assinatura e então clique em **Validar Assinatura**.  
  
4.  Na caixa de diálogo **Validar Assinatura** , selecione **Validar esta assinatura**.  
  
5.  Para especificar o tipo de validação a ser executado (contagem de linha ou contagem de linha e soma de verificação) clique em **Opções**e então especifique as opções na caixa de diálogo **Opções de Validação de Assinatura** .  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Exiba os resultados da validação no Replication Monitor ou a caixa de diálogo **Exibir Status da Sincronização** :  
  
    1.  Expanda a publicação, clique com o botão direito do mouse na assinatura e então clique em **Exibir Status da Sincronização**.  
  
    2.  Se o agente não estiver sendo executado clique em **Iniciar** na caixa de diálogo **Exibir Status da Sincronização** . A caixa de diálogo exibirá mensagens informativas relacionadas à validação.  
  
     Se você não vir nenhuma mensagem relacionada à validação, o agente já registrou uma mensagem subsequente. Neste caso, exiba os resultados de validação no Replication Monitor. Para obter mais informações, consulte os procedimentos de instruções do Replication Monitor neste tópico.  
  
#### <a name="to-validate-data-for-all-subscriptions-to-a-merge-publication-management-studio"></a>Para validar dados para todas as assinaturas para uma publicação de mesclagem (Management Studio)  
  
1.  Conecte-se ao Publicador no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse na publicação para a qual você quer validar assinaturas e então clique em **Validar Todas as Assinaturas**.  
  
4.  Na caixa de diálogo **Validar Todas as Assinaturas** , especifique o tipo de validação a ser executado (contagem de linha ou contagem de linha e soma de verificação).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Exiba os resultados da validação no Replication Monitor ou a caixa de diálogo **Exibir Status da Sincronização** . Para cada assinatura:  
  
    1.  Expanda a publicação, clique com o botão direito do mouse na assinatura e então clique em **Exibir Status da Sincronização**.  
  
    2.  Se o agente não estiver sendo executado clique em **Iniciar** na caixa de diálogo **Exibir Status da Sincronização** . A caixa de diálogo exibirá mensagens informativas relacionadas à validação.  
  
     Se você não vir nenhuma mensagem relacionada à validação, o agente já registrou uma mensagem subsequente. Neste caso, exiba os resultados de validação no Replication Monitor. Para obter mais informações, consulte os procedimentos de instruções do Replication Monitor neste tópico.  
  
#### <a name="to-validate-data-for-all-push-subscriptions-to-a-transactional-publication-replication-monitor"></a>Para validar dados para todas as inscrições push para uma publicação transacional (Replication Monitor)  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo e, depois, expanda um Publicador.  
  
2.  Clique com o botão direito do mouse na publicação para a qual você quer validar assinaturas e então clique em **Validar Assinaturas**.  
  
3.  Na caixa de diálogo **Validar Assinaturas** , selecione quais assinatura validar:  
  
    -   Selecione **Validar todas as assinaturas SQL Server**  
  
    -   Selecione **Validar estas assinaturas**e então selecione uma ou mais assinaturas.  
  
4.  Para especificar o tipo de validação a ser executado (contagem de linha ou contagem de linha e soma de verificação) clique em **Opções de Validação**e então especifique as opções na caixa de diálogo **Opções de Validação de Assinatura** .  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Clique na guia **Todas as Assinaturas** .  
  
7.  Exiba os resultados da validação. Para cada assinatura push:  
  
    1.  Se o agente não estiver sendo executado, clique com o botão direito do mouse na assinatura e então clique em **Iniciar Sincronização**.  
  
    2.  Clique com o botão direito do mouse na assinatura e, em seguida, clique em **Exibir Detalhes**.  
  
    3.  Exiba informações na guia **Histórico de Distribuidor para o Assinante** na área de texto **Ações na seção selecionada** .  
  
#### <a name="to-validate-data-for-a-single-push-subscription-to-a-merge-publication-replication-monitor"></a>Para validar dados para uma única assinatura push para uma publicação de mesclagem (Replication Monitor)  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo, expanda um Publicador e, depois, clique em uma publicação.  
  
2.  Clique na guia **Todas as Assinaturas** .  
  
3.  Clique com o botão direito do mouse na assinatura que você quer validar, depois clique em **Validar Assinatura**.  
  
4.  Na caixa de diálogo **Validar Assinatura** , selecione **Validar esta assinatura**.  
  
5.  Para especificar o tipo de validação a ser executado (contagem de linha ou contagem de linha e soma de verificação) clique em **Opções**e então especifique as opções na caixa de diálogo **Opções de Validação de Assinatura** .  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  Clique na guia **Todas as Assinaturas** .  
  
8.  Exiba os resultados da validação:  
  
    1.  Se o agente não estiver sendo executado, clique com o botão direito do mouse na assinatura e então clique em **Iniciar Sincronização**.  
  
    2.  Clique com o botão direito do mouse na assinatura e, em seguida, clique em **Exibir Detalhes**.  
  
    3.  Exiba informações na guia **Histórico de Sincronização** na área de texto **Última mensagem da sessão selecionada** .  
  
#### <a name="to-validate-data-for-all-push-subscriptions-to-a-merge-publication-replication-monitor"></a>Para validar dados para todas as assinaturas push para uma publicação de mesclagem (Replication Monitor)  
  
1.  No Replication Monitor, expanda um Grupo do publicador no painel esquerdo e, depois, expanda um Publicador.  
  
2.  Clique com o botão direito do mouse na publicação para a qual você quer validar assinaturas e então clique em **Validar Todas as Assinaturas**.  
  
3.  Na caixa de diálogo **Validar Todas as Assinaturas** , especifique o tipo de validação a ser executado (contagem de linha ou contagem de linha e soma de verificação).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  Clique na guia **Todas as Assinaturas** .  
  
6.  Exiba os resultados da validação. Para cada assinatura push:  
  
    1.  Se o agente não estiver sendo executado, clique com o botão direito do mouse na assinatura e então clique em **Iniciar Sincronização**.  
  
    2.  Clique com o botão direito do mouse na assinatura e, em seguida, clique em **Exibir Detalhes**.  
  
    3.  Exiba informações na guia **Histórico de Sincronização** na área de texto **Última mensagem da sessão selecionada** .  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>Para validar dados para todos os artigos em uma publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md). Especifique **@publication** e um dos valores seguintes para **@rowcount_only**:  
  
    -   **1** - apenas verifica número de linhas (o padrão)  
  
    -   **2** - número de linhas e soma de verificação binária.  
  
    > [!NOTE]  
    >  Ao executar [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md), [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) é executado para cada artigo na publicação. Para executar [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md) com êxito, é necessário ter permissões SELECT em todas as colunas nas tabelas base publicadas.  
  
2.  (Opcional) Iniciar o Distribution Agent para cada assinatura se já não estiver em execução. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Verifique a saída de agente para o resultado da validação. Para obter mais informações, consulte [Validar os dados replicados](../../relational-databases/replication/validate-replicated-data.md).  
  
#### <a name="to-validate-data-for-a-single-article-in-a-transactional-publication"></a>Para validar dados para um único artigo em uma publicação transacional  
  
1.  No Publicador no banco de dados de publicação, execute [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md). Especifique **@publication**, o nome do artigo como **@article**e um dos valores seguintes como **@rowcount_only**:  
  
    -   **1** - apenas verifica número de linhas (o padrão)  
  
    -   **2** - número de linhas e soma de verificação binária.  
  
    > [!NOTE]  
    >  Para executar [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) com êxito, é necessário ter permissões SELECT em todas as colunas na tabela base publicada.  
  
2.  (Opcional) Iniciar o Distribution Agent para cada assinatura se já não estiver em execução. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Verifique a saída de agente para o resultado da validação. Para obter mais informações, consulte [Validar os dados replicados](../../relational-databases/replication/validate-replicated-data.md).  
  
#### <a name="to-validate-data-for-a-single-subscriber-to-a-transactional-publication"></a>Para validar dados de um único assinante para uma publicação transacional  
  
1.  No Publicador do banco de dados de publicação, abra uma transação explícita usando [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md).  
  
2.  No Publicador no banco de dados de publicação, execute [sp_marksubscriptionvalidation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md). Especifique a publicação como **@publication**, o nome do Assinante como **@subscriber**, e o nome do banco de dados da assinatura como **@destination_db**.  
  
3.  (Opcional) Repita a etapa 2 para cada assinatura que é validada.  
  
4.  No Publicador no banco de dados de publicação, execute [sp_article_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md). Especifique **@publication**, o nome do artigo como **@article**e um dos valores seguintes como **@rowcount_only**:  
  
    -   **1** - apenas verifica número de linhas (o padrão)  
  
    -   **2** - número de linhas e soma de verificação binária.  
  
    > [!NOTE]  
    >  Para executar [sp_publication_validation &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) com êxito, é necessário ter permissões SELECT em todas as colunas na tabela base publicada.  
  
5.  No Publicador do banco de dados de publicação, confirme a transação usando [COMMIT TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-transaction-transact-sql.md).  
  
6.  (Opcional) Repita as etapas 1 a 5 para cada artigo que é validado.  
  
7.  (Opcional) Iniciar o Distribution Agent se já não estiver em execução. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
8.  Verifique a saída de agente para o resultado da validação. Para obter mais informações, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>Para validar dados em todas as assinaturas para uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_validatemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md). Especifique **@publication** e um dos valores seguintes para **@level**:  
  
    -   **1** - apenas validação de número de linhas.  
  
    -   **3** - validação de soma de verificação binária de número de linhas.  
  
     Isso marca todas as assinaturas para validação.  
  
2.  Inicie o agente de mesclagem para cada assinatura. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Verifique a saída de agente para o resultado da validação. Para obter mais informações, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md).  
  
#### <a name="to-validate-data-in-selected-subscriptions-to-a-merge-publication"></a>Para validar dados nas assinaturas selecionadas para uma publicação de mesclagem  
  
1.  No Publicador no banco de dados de publicação, execute [sp_validatemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md). Especifique **@publication**, o nome do Assinante como **@subscriber**, o nome do banco de dados de assinatura como **@subscriber_db**e um dos valores seguintes como **@level**:  
  
    -   **1** - apenas validação de número de linhas.  
  
    -   **3** - validação de soma de verificação binária de número de linhas.  
  
     Isso marca a assinatura selecionada para validação.  
  
2.  Inicie o agente de mesclagem para cada assinatura. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
3.  Verifique a saída de agente para o resultado da validação.  
  
4.  Repita as etapas 1 a 3 para cada assinatura que é validada.  
  
> [!NOTE]  
>  A assinatura para uma publicação de mesclagem também pode ser validada especificando-se o parâmetro **-Validate** ao executar o [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md).  
  
#### <a name="to-validate-data-in-a-subscription-using-merge-agent-parameters"></a>Para validar dados em uma assinatura usando parâmetros do Merge Agent  
  
1.  Inicie o Merge Agent no Assinante (assinatura pull) ou no Distribuidor (assinatura push) do prompt de comando em um dos seguintes modos.  
  
    -   Especificando o valor de **1** (número de linhas) ou **3** (número de linhas e soma de verificação binária) para o parâmetro **-Validate** .  
  
    -   Especificando **validação de número de linhas** ou **validação de número de linhas e de soma de verificação** para o parâmetro **- ProfileName** .  
  
     Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) ou [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
##  <a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
 A replicação permite que você use RMO (Replication Management Objects) para validar programaticamente os dados que no Assinante correspondam aos dados do Publicador. Os objetos usados dependem do tipo de topologia de replicação. A replicação transacional necessita de validação em todas as assinaturas de uma publicação.  
  
> [!NOTE]  
>  Para obter um exemplo, consulte [Exemplo (RMO)](#RMOExample)posteriormente nesta seção.  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>Para validar dados para todos os artigos em uma publicação transacional  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.TransPublication> . Defina as propriedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação. Defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades remanescentes do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A> . Passe o seguinte:  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>  
  
    -   Um Booliano que indica se é preciso parar o Distribution Agent depois de completar a validação.  
  
     Isso marca os artigos para a validação.  
  
5.  Se ainda não estiver executando, inicie o Distribution Agent para sincronizar cada assinatura. Para obter mais informações, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) ou [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md). O resultado da operação de validação é escrito no histórico do agente. Para obter mais informações, consulte [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>Para validar dados em todas as assinaturas para uma publicação de mesclagem  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> . Defina as propriedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação. Defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades remanescentes do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A> . Passe o <xref:Microsoft.SqlServer.Replication.ValidationOption>desejado.  
  
5.  Execute o Merge Agent para cada assinatura iniciar a validação ou espere pela próxima execução de agente marcada. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md). O resultado da operação de validação é gravado no histórico de agente que você exibe usando o Replication Monitor. Para obter mais informações, consulte [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
#### <a name="to-validate-data-in-a-single-subscription-to-a-merge-publication"></a>Para validar os dados em uma única assinatura em uma publicação de mesclagem  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Crie uma instância da classe <xref:Microsoft.SqlServer.Replication.MergePublication> . Defina as propriedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> e <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para a publicação. Defina a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> para a conexão criada na etapa 1.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades remanescentes do objeto. Se esse método retornar **false**, as propriedades de publicação na etapa 2 foram definidas incorretamente ou a publicação não existe.  
  
4.  Chame o método <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A> . Passe o nome do Assinante e banco de dados de assinatura que estão sendo validados e o <xref:Microsoft.SqlServer.Replication.ValidationOption>desejado.  
  
5.  Execute o Merge Agent para a assinatura iniciar a validação ou espere pela próxima execução de agente marcada. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) e [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md). O resultado da operação de validação é gravado no histórico de agente que você exibe usando o Replication Monitor. Para obter mais informações, consulte [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md).  
  
###  <a name="RMOExample"></a> Exemplo (RMO)  
 Este exemplo marca todas as assinatura em uma publicação transacional para a validação de número de linhas.  
  
 [!code-cs[HowTo#rmo_ValidateTranPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 Este exemplo marca uma assinatura específica em uma publicação de mesclagem para validação de número de linhas.  
  
 [!code-cs[HowTo#rmo_ValidateMergeSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
  
