---
title: Gerenciar uma instância CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- manIns
ms.assetid: cfed22c8-c666-40ca-9e73-24d93e85ba92
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8840756a2036b5c2a62d2aa456773a46167a51fe
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="manage-a-cdc-instance"></a>Gerenciar uma instância CDC
  Você pode usar o CDC Designer Console para exibir informações sobre as instâncias que você cria e gerenciar a operação das instâncias.  
  
 Clique no nome de uma instância no painel esquerdo para exibir as informações sobre a instância.  
  
> [!NOTE]  
>  Se você selecionar um serviço no painel esquerdo, a lista de instâncias disponíveis também será exibida no centro do CDC Designer Console. Se você selecionar uma das instâncias nesta seção, poderá realizar as tarefas no painel direito; porém, você não poderá exibir as informações nas guias de propriedade.  
  
## <a name="what-you-can-do-when-you-display-the-cdc-instance-information"></a>O que você pode fazer quando exibe as informações da Instância CDC  
 As ações a seguir são realizadas no painel direito:  
  
 **Iniciar**  
 Clique em **Iniciar** para iniciar a capturar alterações para a instância CDC selecionada.  
  
 **Parar**  
 Clique em **Parar** para parar de capturar alterações para a instância CDC selecionada. Quando você para a instância de CDC, as alterações que foram capturadas naquele ponto não são perdidas e são entregues quando a instância CDC é retomada.  
  
 **Redefinir**  
 Clique em **Redefinir** para redefinir a instância CDC a seu estado inicial (vazio). Esta opção está disponível quando a instância CDC é parada. Todas as alterações nas tabelas de alteração e o estado interno da instância CDC são excluídos. Quando a instância CDC é iniciada posteriormente, a captura de alterações inicia a partir desse ponto no tempo e só inclui transações iniciadas depois que a instância CDC iniciou.  
  
 Clique em **OK** na caixa de diálogo de confirmação para confirmar que você deseja redefinir a instância CDC e excluir as alterações gravadas nas tabelas de alteração.  
  
 **Delete (excluir)**  
 Clique em **Excluir** para excluir a instância CDC permanentemente. Esta opção está disponível somente quando a instância CDC é parada.  
  
 Clique em **OK** na caixa de diálogo de confirmação para confirmar que você deseja excluir a instância CDC.  
  
 **Script de registro em log do Oracle**  
 Clique neste link para exibir a caixa de diálogo do script de registro em log do Oracle com o script de registro em log suplementar do Oracle. Para obter informações sobre o que você pode fazer nesta caixa de diálogo, consulte [Oracle Supplemental Logging Script](../../integration-services/change-data-capture/oracle-supplemental-logging-script.md).  
  
> [!NOTE]  
>  Quando você executa os scripts de log suplementares, a caixa de diálogo Oracle Credentials for Running Script abre e você fornece um nome de usuário e senha do Oracle válidos. Para obter informações sobre como fornecer as credenciais corretas do Oracle, consulte [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md).  
  
 **Script de implantação de instância CDC**  
 Clique neste link para exibir a caixa de diálogo CDC Instance Deployment Script que exibe o script de implantação de instância CDC. Para obter informações sobre essa caixa de diálogo, consulte [CDC Instance Deployment Script](../../integration-services/change-data-capture/cdc-instance-deployment-script.md).  
  
 **Propriedades**  
 Clique neste link para abrir o editor de propriedades. Você edita a configuração da instância CDC usando o editor de propriedade. Para obter mais informações sobre edição de propriedades para uma instância CDC, consulte [Edit Instance Properties](../../integration-services/change-data-capture/edit-instance-properties.md).  
  
 **Guias do Visualizador**  
  
 As guias do Visualizador a seguir estão disponíveis quando você exibe informações para a instância CDC. As informações nessas guias são somente leitura.  
  
 **Status**  
 Esta guia fornece informações e estatísticas sobre o status atual da instância CDC. Ele contém as informações a seguir.  
  
-   **Status**: um ícone que indica o status atual para a instância CDC. A seguir veja a descrição dos status.  
  
    |||  
    |-|-|  
    |![Error](../../integration-services/change-data-capture/media/error.gif "Error")|**Error**. A Instância Oracle CDC não está sendo executada devido a um erro não reproduzível. Os seguintes substatus estão disponíveis:<br /><br /> **Misconfigured**: um erro de configuração ocorrido que exige intervenção manual.<br /><br /> **Password Required**: nenhuma senha foi definida para a Instância Oracle CDC ou a senha não é válida.<br /><br /> **Unexpected**. Todos os outros erros não recuperáveis.|  
    |![OK](../../integration-services/change-data-capture/media/okay.gif "OK")|**Running**: a instância CDC está sendo executada e está processando registros de alteração. Os seguintes substatus estão disponíveis:<br /><br /> **Idle**: Todos os registros de alteração foram processados e armazenados nas tabelas de alteração de destino. Não há mais nenhuma transação ativa.<br /><br /> **Processing**: há registros de alteração sendo processados que ainda não estão gravados nas tabelas de alteração.|  
    |![Parar](../../integration-services/change-data-capture/media/stop.gif "Parar")|**Stopped**: a instância CDC não está em execução. O status Stopped indica que a instância CDC foi parada de uma maneira normal.|  
    |![Paused](../../integration-services/change-data-capture/media/paused.gif "Paused")|**Paused**: a instância de CDC está sendo executada, mas o processamento está suspenso devido a um erro reproduzível. Os seguintes substatus estão disponíveis:<br /><br /> **Disconnected**: a conexão ao banco de dados Oracle de origem não pode ser estabelecida. O processamento será retomado quando a conexão for restaurada.<br /><br /> **Storage**: o armazenamento está completo. O processamento será retomado quando um armazenamento adicional estiver disponível.<br /><br /> **Agente**: o agente está conectado ao Oracle, mas não pode ler os logs de transação do Oracle devido a um problema temporário, por exemplo, um log de transação necessário não está disponível.|  
  
-   **Detailed Status**: o substatus atual.  
  
-   **Status Message**: mais informações sobre o status atual.  
  
-   **Timestamp**: a hora UTC para quando o estado CDC foi lido pela última vez na tabela de estado.  
  
-   **Currently Processing**: você monitora as informações a seguir nesta seção.  
  
    -   **Last transaction timestamp**: a hora local da última transação que foi gravada nas tabelas de alteração.  
  
    -   **Last change timestamp**: a hora local da alteração mais recente vista pela Instância Oracle CDC nos logs de transação do banco de dados Oracle de origem. Isto fornece informações sobre a latência atual da instância CDC ao ler o log de transação do Oracle.  
  
    -   **CN de cabeçalho de log de transação**: o número de alteração mais recente (CN) foi lido do log de transação do Oracle.  
  
    -   **Transaction log tail CN**: o número de alteração para recuperar ou reiniciar a instância CDC. A instância Oracle CDC vai ser reposicionada neste local no caso de uma reinicialização ou qualquer outro tipo de falha (inclusive failover de cluster).  
  
    -   **CN Atual**: o último número de alteração (SCN) visto no banco de dados Oracle de origem (não o log de transação).  
  
    -   **Transações ativas**: o número atual de transações do Oracle de origem que estão sendo processadas pela Instância Oracle CDC e que ainda não foram decididas (confirmar/reverter).  
  
    -   **Transações preparadas**: o número atual de transações Oracle de origem preparadas para a tabela [cdc.xdbcdc_staged_transactions](../../integration-services/change-data-capture/the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions) .  
  
-   **Contadores**: você monitora as informações a seguir nesta seção.  
  
    -   **Completed transactions**: o número de transações concluídas desde que a instância CDC foi reiniciada pela última vez. Isto não inclui transações que não contêm tabelas de interesse.  
  
    -   **Written changes**: o número de alterações gravadas nas tabelas de alteração do SQL Server.  
  
 **Oracle**  
 Exibe informações sobre a instância CDC e sua conexão com o banco de dados Oracle. Esta guia é somente leitura. Para editar essas propriedades, clique com o botão direito do mouse na instância do painel esquerdo e selecione **Propriedades** ou clique em **Propriedades** no painel direito para abrir a caixa de diálogo Propriedades de \<instância>.  
  
 Para obter mais informações sobre essas propriedades e como editá-las, consulte [Edit the Oracle Database Properties](../../integration-services/change-data-capture/edit-the-oracle-database-properties.md).  
  
 **Tabelas**  
 Exibe informações sobre as tabelas incluídas na instância CDC. As informações sobre colunas também estão disponíveis aqui. Esta guia é somente leitura. Para editar essas propriedades, clique com o botão direito do mouse na instância do painel esquerdo e selecione **Propriedades** ou clique em **Propriedades** no painel direito para abrir a caixa de diálogo Propriedades de \<instância>.  
  
 Para obter mais informações sobre essas propriedades e como editá-las, consulte [Edit Tables](../../integration-services/change-data-capture/edit-tables.md).  
  
 **Avançado**  
 Exibe as propriedades avançadas para a instância CDC e os valores de propriedade. Esta guia é somente leitura. Para editar essas propriedades, clique com o botão direito do mouse na instância do painel esquerdo e selecione **Propriedades** ou clique em **Propriedades** no painel direito para abrir a caixa de diálogo Propriedades de \<instância>.  
  
 Para obter mais informações sobre essas propriedades e como editá-las, consulte [Edit the Advanced Properties](../../integration-services/change-data-capture/edit-the-advanced-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Como criar a instância de banco de dados de alteração do SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Como exibir as propriedades de instância CDC](../../integration-services/change-data-capture/how-to-view-the-cdc-instance-properties.md)   
 [Como editar as propriedades de instância CDC](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [Usar o assistente para nova instância](../../integration-services/change-data-capture/use-the-new-instance-wizard.md)  
  
  
