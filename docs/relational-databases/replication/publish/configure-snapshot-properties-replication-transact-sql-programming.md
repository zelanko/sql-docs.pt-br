---
title: "Configurar propriedades de instant&#226;neo (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "instantâneos [replicação do SQL Server], propriedades"
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# Configurar propriedades de instant&#226;neo (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  Propriedades de instantâneo podem ser definidas e modificadas de forma programada usando-se procedimentos armazenados de replicação, nos quais os procedimentos armazenados usados dependem do tipo de publicação.  
  
### Para configurar propriedades de instantâneo ao criar uma publicação de instantâneo ou transacional  
  
1.  No publicador, execute [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Especifique um nome de publicação para **@publication**, um valor de **instantâneo** ou **contínua** para **@repl_freq**, e um ou mais dos seguintes parâmetros relacionados de instantâneo:  
  
    -   **@alt_snapshot_folder** -Especifique um caminho se o instantâneo desta publicação for acessado daquele local em vez de ou além da pasta de instantâneo padrão.  
  
    -   **@compress_snapshot** -Especifique um valor de **true** se os arquivos de instantâneo na pasta de instantâneo alternativa forem compactados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] formato de arquivo CAB.  
  
    -   **@pre_snapshot_script** -Especifique o nome do arquivo e caminho completo de um **. SQL** arquivo que será executado no assinante durante a inicialização antes do instantâneo inicial é aplicado.  
  
    -   **@post_snapshot_script** -Especifique o nome do arquivo e caminho completo de um **. SQL** arquivo que será executado no assinante durante a inicialização depois que o instantâneo inicial é aplicado.  
  
    -   **@snapshot_in_defaultfolder** -Especifique um valor de **false** se o instantâneo está disponível somente em um local não padrão.  
  
     Para obter mais informações sobre a criação de publicações, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### Para configurar propriedades de instantâneo ao criar uma publicação de mesclagem  
  
1.  No publicador, execute [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique um nome de publicação para **@publication**, um valor de **instantâneo** ou **contínua** para **@repl_freq**, e um ou mais dos seguintes parâmetros relacionados de instantâneo:  
  
    -   **@alt_snapshot_folder** -Especifique um caminho se o instantâneo desta publicação for acessado daquele local em vez de ou além da pasta de instantâneo padrão.  
  
    -   **@compress_snapshot** -Especifique um valor de **true** se os arquivos de instantâneo na pasta de instantâneo alternativa são compactados no formato de arquivo CAB.  
  
    -   **@pre_snapshot_script** -Especifique o nome do arquivo e caminho completo de um **. SQL** arquivo que será executado no assinante durante a inicialização antes do instantâneo inicial é aplicado.  
  
    -   **@post_snapshot_script** -Especifique o nome do arquivo e caminho completo de um **. SQL** arquivo que será executado no assinante durante a inicialização depois que o instantâneo inicial é aplicado.  
  
    -   **@snapshot_in_defaultfolder** -Especifique um valor de **false** se o instantâneo está disponível somente em um local não padrão.  
  
2.  Para obter mais informações sobre a criação de publicações, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### Para modificar as propriedades de instantâneo de uma publicação de instantâneo ou transacional existente  
  
1.  No publicador do banco de dados de publicação, execute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Especifique um valor de **1** para **@force_invalidate_snapshot** e um dos seguintes valores para **@property**:  
  
    -   **alt_snapshot_folder** -também especifique um novo caminho para a pasta de instantâneo alternativa para **@value**.  
  
    -   **compress_snapshot** -também especifique um valor de **true** ou **false** para **@value** para indicar se os arquivos de instantâneo na pasta de instantâneo alternativa são compactados no formato de arquivo CAB.  
  
    -   **pre_snapshot_script** - também para **@value** especificar o nome do arquivo e caminho completo de um **. SQL** arquivo que será executado no assinante durante a inicialização antes do instantâneo inicial é aplicado.  
  
    -   **post_snapshot_script** - também para **@value** especificar o nome do arquivo e caminho completo de um **. SQL** arquivo que será executado no assinante durante a inicialização depois que o instantâneo inicial é aplicado.  
  
    -   **snapshot_in_defaultfolder** -também especifique um valor de **true** ou **false** para indicar se o instantâneo está disponível somente em um local não padrão.  
  
2.  (Opcional) No publicador do banco de dados de publicação, execute [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md). Especifique **@publication** e um ou mais dos parâmetros de credencial de segurança ou programação que está sendo alterados.  
  
    > [!IMPORTANT]  
    >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
3.  Execute o [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) do prompt de comando ou iniciar o trabalho do Snapshot Agent para gerar um novo instantâneo. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
### Para modificar as propriedades de instantâneo de uma publicação de mesclagem existente  
  
1.  No publicador do banco de dados de publicação, execute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique um valor de **1** para **@force_invalidate_snapshot** e um dos seguintes valores para **@property**:  
  
    -   **alt_snapshot_folder** -também especifique um novo caminho para a pasta de instantâneo alternativa para **@value**.  
  
    -   **compress_snapshot** -também especifique um valor de **true** ou **false** para **@value** para indicar se os arquivos de instantâneo na pasta de instantâneo alternativa são compactados no formato de arquivo CAB.  
  
    -   **pre_snapshot_script** - também para **@value** especificar o nome do arquivo e caminho completo de um **. SQL** arquivo que será executado no assinante durante a inicialização antes do instantâneo inicial é aplicado.  
  
    -   **post_snapshot_script** - também para **@value** especificar o nome do arquivo e caminho completo de um **. SQL** arquivo que será executado no assinante durante a inicialização depois que o instantâneo inicial é aplicado.  
  
    -   **snapshot_in_defaultfolder** -também especifique um valor de **true** ou **false** para indicar se o instantâneo está disponível somente em um local não padrão.  
  
2.  Execute o [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) do prompt de comando ou iniciar o trabalho do Snapshot Agent para gerar um novo instantâneo. Para obter mais informações, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## Exemplo  
 Esse exemplo cria uma publicação que usa uma pasta de instantâneo alternativa e um instantâneo compactado.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## Consulte também  
 [Locais da pasta de instantâneos alternativos](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)   
 [Instantâneos compactados](../../../relational-databases/replication/compressed-snapshots.md)   
 [Executar scripts antes e depois da aplicação do instantâneo](../../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Conceitos dos procedimentos armazenados do sistema de replicação](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantâneos pelo FTP](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  