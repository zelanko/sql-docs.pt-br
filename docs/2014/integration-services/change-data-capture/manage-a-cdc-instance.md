---
title: Gerenciar uma instância CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- manIns
ms.assetid: cfed22c8-c666-40ca-9e73-24d93e85ba92
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e4a563a47500a329a79513afb83aff4f93ebda7e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52748258"
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
 Clique neste link para exibir a caixa de diálogo do script de registro em log do Oracle com o script de registro em log suplementar do Oracle. Para obter informações sobre o que você pode fazer nesta caixa de diálogo, consulte [Oracle Supplemental Logging Script](oracle-supplemental-logging-script.md).  
  
> [!NOTE]  
>  Quando você executa os scripts de log suplementares, a caixa de diálogo Oracle Credentials for Running Script abre e você fornece um nome de usuário e senha do Oracle válidos. Para obter informações sobre como fornecer as credenciais corretas do Oracle, consulte [Oracle Credentials for Running Script](oracle-credentials-for-running-script.md).  
  
 **Script de implantação de instância CDC**  
 Clique neste link para exibir a caixa de diálogo CDC Instance Deployment Script que exibe o script de implantação de instância CDC. Para obter informações sobre essa caixa de diálogo, consulte [CDC Instance Deployment Script](cdc-instance-deployment-script.md).  
  
 **Propriedades**  
 Clique neste link para abrir o editor de propriedades. Você edita a configuração da instância CDC usando o editor de propriedade. Para obter mais informações sobre edição de propriedades para uma instância CDC, consulte [Edit Instance Properties](edit-instance-properties.md).  
  
 **Guias do Visualizador**  
  
 As guias do Visualizador a seguir estão disponíveis quando você exibe informações para a instância CDC. As informações nessas guias são somente leitura.  
  
 **Status**  
 Esta guia fornece informações e estatísticas sobre o status atual da instância CDC. Ele contém as informações a seguir.  
  
-   **status**: Um ícone que indica o status atual para a instância CDC. A seguir veja a descrição dos status.  
  
    |||  
    |-|-|  
    |![Error](../media/error.gif "Error")|**Error**. A Instância Oracle CDC não está sendo executada devido a um erro não reproduzível. Os seguintes substatus estão disponíveis:<br /><br /> **Configurado incorretamente**: Ocorreu um erro de configuração que exige intervenção manual.<br /><br /> **Senha necessária**: Nenhuma senha foi definida para a instância Oracle CDC ou a senha não é válida.<br /><br /> **Unexpected**. Todos os outros erros não recuperáveis.|  
    |![OK](../media/okay.gif "OK")|**Executando**: A instância CDC está em execução e está processando registros de alteração. Os seguintes substatus estão disponíveis.<br /><br /> **Idle**: Todos os registros de alteração foram processados e armazenados nas tabelas de alteração de destino. Não há mais nenhuma transação ativa.<br /><br /> **Processamento**: Há registros de alteração sendo processados que ainda não estão gravados nas tabelas de alteração.|  
    |![Parar](../media/stop.gif "Parar")|**Parado**: A instância CDC não está em execução. O status Stopped indica que a instância CDC foi parada de uma maneira normal.|  
    |![Paused](../media/paused.gif "Paused")|**Em pausa**: A instância CDC está em execução, mas o processamento está suspenso devido a um erro reproduzível. Os seguintes substatus estão disponíveis:<br /><br /> **Desconectado**: Não é possível estabelecer a conexão à fonte de dados Oracle. O processamento será retomado quando a conexão for restaurada.<br /><br /> **Armazenamento**: O armazenamento está cheio. O processamento será retomado quando um armazenamento adicional estiver disponível.<br /><br /> **Agente de log**: O agente está conectado ao Oracle, mas não é possível ler os logs de transação do Oracle devido a um problema temporário, por exemplo, um log de transação necessário não está disponível.|  
  
-   **Status detalhado**: O substatus atual.  
  
-   **Mensagem de status**: Mais informações sobre o status atual.  
  
-   **Carimbo de hora**: A hora de UTC para quando o estado CDC foi lido pela última vez da tabela de estado.  
  
-   **Atualmente, o processamento**: Você monitorar as informações a seguir nesta seção.  
  
    -   **Carimbo de hora do última transação**: A hora local da última transação gravada nas tabelas de alteração.  
  
    -   **Última alteração timestamp**: A hora local da alteração mais recente Vista pela instância Oracle CDC nos logs de transação de banco de dados Oracle de origem. Isto fornece informações sobre a latência atual da instância CDC ao ler o log de transação do Oracle.  
  
    -   **CN de cabeçalho do log de transação**: O número mais recente alteração (CN) que foi lido do log de transação do Oracle.  
  
    -   **Parte final do log de transação CN**: O número de alteração para recuperar ou reiniciar a instância CDC. A instância Oracle CDC vai ser reposicionada neste local no caso de uma reinicialização ou qualquer outro tipo de falha (inclusive failover de cluster).  
  
    -   **CN atual**: O último número de alteração (SCN) visto do banco de dados do Oracle de origem (não o log de transações).  
  
    -   **Transações ativas**: O número atual de transações Oracle de origem que estão sendo processadas pela instância Oracle CDC e não foram decididas (confirmar/reverter).  
  
    -   **Transações preparadas**: As número atual fonte Oracle de transações preparadas para o [xdbcdc_staged_transactions](the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_staged_transactions) tabela.  
  
-   **Contadores de**: Você monitorar as informações a seguir nesta seção.  
  
    -   **Transações concluídas**: O número de transações concluídas desde que a instância CDC foi reiniciada pela última vez. Isto não inclui transações que não contêm tabelas de interesse.  
  
    -   **Escrito alterações**: O número de alterações gravadas para o SQL Server nas tabelas de alteração.  
  
 **Oracle**  
 Exibe informações sobre a instância CDC e sua conexão com o banco de dados Oracle. Esta guia é somente leitura. Para editar essas propriedades, clique com o botão direito do mouse na instância do painel esquerdo e selecione **Propriedades** ou clique em **Propriedades** no painel direito para abrir a caixa de diálogo Propriedades de \<instância>.  
  
 Para obter mais informações sobre essas propriedades e como editá-las, consulte [Edit the Oracle Database Properties](edit-the-oracle-database-properties.md).  
  
 **Tabelas**  
 Exibe informações sobre as tabelas incluídas na instância CDC. As informações sobre colunas também estão disponíveis aqui. Esta guia é somente leitura. Para editar essas propriedades, clique com o botão direito do mouse na instância do painel esquerdo e selecione **Propriedades** ou clique em **Propriedades** no painel direito para abrir a caixa de diálogo Propriedades de \<instância>.  
  
 Para obter mais informações sobre essas propriedades e como editá-las, consulte [Edit Tables](edit-tables.md).  
  
 **Avançado**  
 Exibe as propriedades avançadas para a instância CDC e os valores de propriedade. Esta guia é somente leitura. Para editar essas propriedades, clique com o botão direito do mouse na instância do painel esquerdo e selecione **Propriedades** ou clique em **Propriedades** no painel direito para abrir a caixa de diálogo Propriedades de \<instância>.  
  
 Para obter mais informações sobre essas propriedades e como editá-las, consulte [Edit the Advanced Properties](edit-the-advanced-properties.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como criar a instância de banco de dados de alteração do SQL Server](how-to-create-the-sql-server-change-database-instance.md)   
 [Como exibir as propriedades de instância CDC](how-to-view-the-cdc-instance-properties.md)   
 [Como editar as propriedades de instância CDC](how-to-edit-the-cdc-instance-properties.md)   
 [Usar o assistente para nova instância](use-the-new-instance-wizard.md)  
  
  
