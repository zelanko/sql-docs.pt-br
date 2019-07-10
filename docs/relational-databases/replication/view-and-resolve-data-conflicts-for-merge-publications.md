---
title: Exibir e resolver conflitos de dados para publicações de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8a5aced367f3b046473887999ff8e72b24ff8156
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2019
ms.locfileid: "67580455"
---
# <a name="conflict-resolution-for-merge-replication"></a>Resolução de conflitos para replicação de mesclagem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os conflitos em replicação de mesclagem são resolvidos baseado no resolvedor especificado para cada artigo. Por padrão, os conflitos são resolvidos sem a necessidade da intervenção do usuário. Mas os conflitos podem ser exibidos e o resultado da resolução poderá ser alterado no Visualizador de Conflitos de Replicação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Os dados de conflito são disponíveis no Visualizador de Conflitos de Replicação pelo período de tempo especificado para o período de retenção de conflito (com um padrão de 14 dias). Para definir o período de retenção de conflito, ou:  
  
-   Especificar um valor de retenção para o **@conflict_retention** parâmetro de [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
-   Especificar o valor de **conflict_retention** para o parâmetro **@property** e um valor de retenção para o parâmetro **@value** de [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 Por padrão, as informações sobre conflitos são armazenadas:    
-   No Publicador e no Assinante, caso o nível de compatibilidade da publicação for 90RTM ou superior.   
-   No Publicador, caso o nível de compatibilidade da publicação seja inferior a 80RTM.   
-   No Publicador, caso os Assinantes estejam executando [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Os dados de conflito não podem ser armazenados nos Assinantes do [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
 O armazenamento de informações sobre conflitos é controlado pela propriedade de publicação de **conflict_logging** . Para obter mais informações, consulte [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) e [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 Os conflitos também podem ser resolvidos interativamente durante a sincronização usando o Resolvedor Interativo da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . O Resolvedor Interativo está disponível pelo Gerenciador de Sincronização do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Para obter mais informações, consulte [Como sincronizar uma assinatura usando o Gerenciador de Sincronização do Windows &#40;Gerenciador de Sincronização do Windows&#41;](../../relational-databases/replication/synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
## <a name="resolve-conflicts"></a>Resolver conflitos  
  
1.  Conecte-se ao Publicador (ou Assinante se apropriado) no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com o botão direito do mouse na publicação para a qual você quer exibir conflitos e então clique em **Exibir Conflitos**.  
  
    > [!NOTE]  
    >  Se você tiver especificado um valor de **'subscriber'** para a propriedade **conflict_logging** , a opção de menu **Exibir Conflitos** não estará disponível. Para exibir conflitos, inicie o ConflictViewer.exe no prompt de comando. Por padrão, ConflictViewer.exe está localizado no seguinte diretório: Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE. Para obter uma lista de parâmetros de inicialização válidos, execute o ConflictViewer.exe -?.  
  
4.  Na caixa de diálogo **Selecionar Tabela de Conflito** , selecione um banco de dados, publicação e tabela para os quais quer exibir conflitos.  
  
5.  No Visualizador de Conflitos de Replicação, é possível:  
  
    -   Filtrar linhas com os botões à direita da grade superior.  
  
    -   Selecionar uma linha na grade superior para exibir informações sobre aquela linha na grade inferior.  
  
    -   Selecionar uma ou mais linhas na grade superior e então clicar em **Remover**, que equivale a clicar no botão **Enviar Vencedor** (sem fazer nenhuma alteração nos dados).  
  
    -   Clique no botão propriedades ( **?** ) para exibir mais informações sobre uma coluna envolvida em um conflito.  
  
    -   Edite dados na coluna **Vencedor do Conflito** ou **Perdedor do Conflito** antes de enviar os dados (os dados são de somente leitura se a coluna estiver cinza).  
  
    -   Clique em **Enviar Vencedor** para aceitar a linha designada como o vencedor do conflito.  
  
    -   Clique em **Enviar Perdedor** para substituir a resolução e propagar o valor designado como o perdedor do conflito para todos os nós da topologia.  
  
    -   Selecione **Registrar os detalhes deste conflito** para registrar dados de conflito em um arquivo. Para especificar um local para o arquivo, aponte para o menu **Exibir** e então clique em **Opções**. Insira um valor ou clique no botão procurar ( **...** ) e então navegue até o arquivo apropriado. Clique em **OK** para sair da caixa de diálogo **Opções** .  
  
6.  Feche o Visualizador de Conflitos de Replicação.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="view-conflict-information"></a>Exibir informações sobre conflitos
Quando um conflito é resolvido em uma replicação de mesclagem, os dados da linha perdedora são gravados em uma tabela de conflitos. Os dados de conflito podem ser visualizados de forma programática, usando procedimentos armazenados de replicação. Para obter mais informações, consulte [Detecção e resolução de conflito de replicação de mesclagem avançada ](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Observe os valores das colunas a seguir no conjunto de resultados.  
  
    -   **centralized_conflicts** - 1 indica que as linhas de conflito são armazenadas no Publicador, e 0 indica que as linhas de conflito não são armazenadas no Publicador.  
  
    -   **decentralized_conflicts** - 1 indica que as linhas de conflito são armazenadas no Assinante e 0 indica que as linhas de conflito não são armazenadas no Assinante.  
  
        > [!NOTE]  
        >  O comportamento do log de conflito de uma publicação de mesclagem é definido, usando-se o parâmetro **@conflict_logging** de [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). O uso do parâmetro **@centralized_conflicts** não está mais em uso.  
  
     A tabela seguinte descreve os valores dessas colunas com base no valor especificado para **@conflict_logging** .  
  
    |@conflict_logging valor|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**Publicador**|1|0|  
    |**Assinante**|0|1|  
    |**ambos**|1|1|  
  
2.  No Publicador do banco de dados de publicação ou no Assinante, no banco de dados da assinatura, execute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique um valor para **@publication** para retornar apenas as informações de conflitos para artigos que pertençam a uma publicação específica. Isso retorna informações da tabela de conflitos para artigos com conflitos. Observe o valor de **conflict_table** para qualquer artigo de interesse. Se o valor de **conflict_table** para um artigo for NULL, só exclua conflitos que tenham ocorrido neste artigo.  
  
3.  (Opcional) Revise linhas de conflito para artigos de interesse. Dependendo dos valores de **centralized_conflicts** e **decentralized_conflicts** de etapa 1, execute um dos seguintes procedimentos:  
  
    -   No Publicador do banco de dados de publicação, execute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique uma tabela de conflitos para o artigo (de etapa 1) para **@conflict_table** . (Opcional) Especifique um valor de **@publication** para restringir informações sobre conflitos retornadas a uma publicação específica. Isso retorna dados de linha e outra informações para a linha perdedora.  
  
    -   No Assinante, no banco de dados da assinatura, execute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique uma tabela de conflitos para o artigo (de etapa 1) para **@conflict_table** . Isso retorna dados de linha e outra informações para a linha perdedora.  
  
## <a name="conflict-where-delete-failed"></a>Conflito em que a exclusão falhou   
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Observe os valores das colunas a seguir no conjunto de resultados.  
  
    -   **centralized_conflicts** - 1 indica que as linhas de conflito são armazenadas no Publicador, e 0 indica que as linhas de conflito não são armazenadas no Publicador.  
  
    -   **decentralized_conflicts** - 1 indica que as linhas de conflito são armazenadas no Assinante e 0 indica que as linhas de conflito não são armazenadas no Assinante.  
  
        > [!NOTE]  
        >  O comportamento do log de conflito de uma publicação de mesclagem é definido usando-se o parâmetro **@conflict_logging** de [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). O uso do parâmetro **@centralized_conflicts** não está mais em uso.  
  
2.  No Publicador do banco de dados de publicação ou no Assinante, no banco de dados da assinatura, execute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique um valor para **@publication** para retornar apenas as informações das tabelas de conflitos para artigos que pertençam a uma publicação específica. Isso retorna informações da tabela de conflitos para artigos com conflitos. Observe o valor de **source_object** para qualquer artigo de interesse. Se o valor de **conflict_table** para um artigo for NULL, só exclua conflitos que tenham ocorrido neste artigo.  
  
3.  (Opcional) Revise informações sobre conflitos para excluir conflitos. Dependendo dos valores de **centralized_conflicts** e **decentralized_conflicts** de etapa 1, execute um dos seguintes procedimentos:  
  
    -   No Publicador do banco de dados de publicação, execute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique o nome da tabela de fonte (da etapa 1) na qual o conflito aconteceu para **@source_object** . (Opcional) Especifique um valor de **@publication** para restringir informações sobre conflitos retornadas a uma publicação específica. Isso retorna informações sobre conflitos de exclusão armazenadas no Publicador.  
  
    -   No Assinante, no banco de dados da assinatura, execute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique o nome da tabela de fonte (da etapa 1) na qual o conflito aconteceu para **@source_object** . (Opcional) Especifique um valor de **@publication** para restringir informações sobre conflitos retornadas a uma publicação específica. Isso retorna informações sobre conflitos de exclusão armazenadas no Assinante.  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Especificar um resolvedor de artigo de mesclagem](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  
