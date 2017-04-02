---
title: "Exibir e resolver conflitos de dados para publica&#231;&#245;es de mesclagem (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "resolução de conflitos de replicação de mesclagem [replicação do SQL Server], visualizando conflitos"
  - "visualizando informações de conflito"
  - "resolução de conflitos [replicação do SQL Server], replicação de mesclagem"
ms.assetid: aeee9546-4480-49f9-8b1e-c71da1f056c7
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Exibir e resolver conflitos de dados para publica&#231;&#245;es de mesclagem (SQL Server Management Studio)
  Os conflitos em replicação de mesclagem são resolvidos baseado no resolvedor especificado para cada artigo. Por padrão, os conflitos são resolvidos sem a necessidade da intervenção do usuário. Mas os conflitos podem ser exibidos e o resultado da resolução poderá ser alterado no Visualizador de Conflitos de Replicação da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 Os dados de conflito são disponíveis no Visualizador de Conflitos de Replicação pelo período de tempo especificado para o período de retenção de conflito (com um padrão de 14 dias). Para definir o período de retenção de conflito, ou:  
  
-   Especifique um valor de retenção para o **@conflict_retention** parâmetro [sp_addmergepublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
-   Especifique um valor de **conflict_retention** para o **@property** parâmetro e uma valor de retenção para o **@value** parâmetro [sp_changemergepublication & 40; O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 Por padrão, as informações sobre conflitos são armazenadas:  
  
-   No Publicador e no Assinante, caso o nível de compatibilidade da publicação for 90RTM ou superior.  
  
-   No Publicador, caso o nível de compatibilidade da publicação seja inferior a 80RTM.  
  
-   No Publicador, caso os Assinantes estejam executando [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Os dados de conflito não podem ser armazenados nos Assinantes do [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
 Armazenamento de informações de conflito é controlado pelo **conflict_logging** a propriedade da publicação. Para obter mais informações, consulte [sp_addmergepublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md) e [sp_changemergepublication & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md).  
  
 Os conflitos também podem ser resolvidos interativamente durante a sincronização usando o Resolvedor Interativo da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . O Resolvedor Interativo está disponível pelo Gerenciador de Sincronização do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Para obter mais informações, consulte [sincronizar uma assinatura usando Windows sincronização Manager & #40. O Gerenciador de sincronização do Windows & 41;](../../relational-databases/replication/synchronize a subscription using windows synchronization manager.md).  
  
### Para exibir e resolver conflitos para publicações de mesclagem  
  
1.  Conectar-se ao publicador (ou assinante se apropriado) em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], e, em seguida, expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, em seguida, a pasta **Publicações Locais** .  
  
3.  Clique com botão direito a publicação para o qual você deseja exibir conflitos e, em seguida, clique em **Exibir conflitos**.  
  
    > [!NOTE]  
    >  Se você tiver especificado um valor de **'assinante'** para o **conflict_logging** propriedade, o **Exibir conflitos** opção de menu não está disponível. Para exibir conflitos, inicie o ConflictViewer.exe no prompt de comando. Por padrão, o ConflictViewer.exe está localizado no seguinte diretório: Microsoft SQL Server\100\Tools\Binn\VSShell\Common7\IDE. Para obter uma lista de parâmetros de inicialização válidos, execute o ConflictViewer.exe -?.  
  
4.  Na caixa de diálogo **Selecionar Tabela de Conflito** , selecione um banco de dados, publicação e tabela para os quais quer exibir conflitos.  
  
5.  No Visualizador de Conflitos de Replicação, é possível:  
  
    -   Filtrar linhas com os botões à direita da grade superior.  
  
    -   Selecionar uma linha na grade superior para exibir informações sobre aquela linha na grade inferior.  
  
    -   Selecione uma ou mais linhas na grade superior e, em seguida, clique em **Remover**, que é equivalente a clicar o **Enviar vencedor** botão (sem fazer quaisquer alterações nos dados).  
  
    -   Clique no botão Propriedades (**...**) exibir mais informações sobre uma coluna envolvido em um conflito.  
  
    -   Editar dados no **vencedor do conflito** ou **perdedor de conflito** coluna antes de enviar os dados (dados serão somente leitura se a coluna estiver cinza).  
  
    -   Clique em **Enviar Vencedor** para aceitar a linha designada como o vencedor do conflito.  
  
    -   Clique em **Enviar Perdedor** para substituir a resolução e propagar o valor designado como o perdedor do conflito para todos os nós da topologia.  
  
    -   Selecione **Registrar os detalhes deste conflito** para registrar dados de conflito em um arquivo. Para especificar um local para o arquivo, aponte para o menu **Exibir** e então clique em **Opções**. Insira um valor ou clique no botão Procurar (**...**) e, em seguida, navegue até o arquivo apropriado. Clique em **OK** para sair da caixa de diálogo **Opções** .  
  
6.  Feche o Visualizador de Conflitos de Replicação.  
  
## Consulte também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada ](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Especificar um resolvedor de artigo de mesclagem](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
  