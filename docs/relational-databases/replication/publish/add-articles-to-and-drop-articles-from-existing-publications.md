---
title: "Adicionar e remover artigos de publica&#231;&#245;es existentes | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "artigos [replicação do SQL Server], descartando"
  - "excluindo artigos"
  - "removendo artigos"
  - "descartando artigos"
  - "adicionando artigos"
  - "administrando a replicação, artigos"
  - "publicações [replicação do SQL Server], adicionando e descartando artigos"
  - "artigos [replicação do SQL Server], adicionando"
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
caps.latest.revision: 48
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 46
---
# Adicionar e remover artigos de publica&#231;&#245;es existentes
  Depois que uma publicação é criada, é possível adicionar e descartar artigos. Os artigos podem ser adicionados a qualquer hora, mas as ações necessárias para descartar artigos dependem do tipo de replicação e de quando o artigo é descartado.  
  
## Adicionando artigos  
 Adicionar um artigo envolve: adicionar o artigo à publicação; criar um novo instantâneo para a publicação; sincronizar a assinatura para aplicar o esquema e os dados para o novo artigo.  
  
> [!NOTE]  
>  Se você adicionar um artigo a uma publicação de mesclagem e depende de um artigo existente o novo artigo, você deve especificar uma ordem de processamento para os dois artigos usando o **@processing_order** parâmetro do [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) e [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Considere o seguinte cenário: uma tabela é publicada, mas não é publicada a função que é referenciada pela tabela. Se a função não for publicada, a tabela não poderá ser criada no Assinante. Quando você adiciona a função à publicação: Especifique um valor de **1** para o **@processing_order** parâmetro do **sp_addmergearticle**; e especifique um valor de **2** para o **@processing_order** parâmetro **sp_changemergearticle**, especificando o nome da tabela para o parâmetro **@article**. Essa ordem de processamento garante a criação da função no Assinante antes da tabela que depende disso. É possível usar números diferentes para cada artigo, desde que o número para a função seja menor que o número para a tabela.  
  
1.  Adicione um ou mais artigos com um dos métodos seguintes:  
  
    -   [Adicionar e remover artigos de uma publicação & #40. SQL Server Management Studio e 41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [Defina um Artigo](../../../relational-databases/replication/publish/define-an-article.md)  
  
2.  Após adicionar um artigo a uma publicação, é necessário criar um novo instantâneo para a publicação (e todas as partições se for uma publicação de mesclagem com filtros com parâmetros). O Agente de Distribuição ou o Agente de Mesclagem então copiará o esquema e os dados para o novo artigo para o Assinante (ele não reinicializa a publicação inteira).  
  
    -   Para criar um novo instantâneo, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   Para criar um novo instantâneo para uma publicação de mesclagem com filtros com parâmetros, consulte [criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
3.  Depois que o instantâneo é criado, sincronize a assinatura para copiar o esquema e os dados para o novo artigo.  
  
    -   Para sincronizar uma inscrição de envio, consulte [sincronizar uma assinatura Push](../../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
    -   Para sincronizar uma assinatura pull, consulte [sincronizar uma assinatura Pull](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
## Descartando artigos  
 Os artigos podem ser descartados de uma publicação a qualquer hora, mas é necessário levar em conta os seguintes comportamentos:  
  
-   Descartar um artigo de uma publicação não remove o objeto do banco de dados de publicação ou o objeto correspondente do banco de dados de assinatura. Use DROP \< objeto> para remover esses objetos, se necessário. Quando você descarta um artigo que está relacionado a outros artigos publicados por meio de restrições de chave estrangeira, recomendamos que você remova a tabela no assinante manualmente ou por meio da execução de script sob demanda: Especifique um script que inclui o DESCARTE apropriado \< objeto> instruções. Para obter mais informações, consulte [Executar Scripts durante a sincronização e 40; Programação Transact-SQL de replicação e 41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   Para publicações de mesclagem com nível de compatibilidade 90RTM ou superior, os artigos podem ser descartados a qualquer hora, porém um novo instantâneo é requerido. Adicionalmente:  
  
    -   Se o artigo é um artigo pai em um filtro de junção ou relação de registro lógico, as relações devem ser descartadas primeiro, o que requer a reinicialização.  
  
    -   Se o artigo tiver o último filtro com parâmetros em uma publicação, as assinaturas deverão ser reinicializadas.  
  
-   Para publicações de mesclagem com nível de compatibilidade inferior a 90RTM, os artigos podem ser descartados sem considerações especiais anteriores à sincronização inicial de assinaturas. Se o artigo for descartado depois que uma ou mais assinaturas forem sincronizadas, as assinaturas devem ser descartadas, recriadas e sincronizadas.  
  
-   Para publicações de instantâneo ou publicações transacionais, os artigos podem ser descartados sem considerações especiais antes de as assinatura serem criadas. Se o artigo for descartado depois que uma ou mais assinaturas forem criadas, as assinaturas devem ser descartadas, recriadas e sincronizadas. Para obter mais informações sobre como remover assinaturas, consulte [assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md) e [sp_dropsubscription & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). **sp_dropsubscription** permite que você soltar um único artigo da assinatura, em vez de toda a assinatura.  
  
1.  Descartar um artigo de uma publicação envolve descartar o artigo e criar um novo instantâneo para a publicação. Descartar um artigo invalida o instantâneo atual; consequentemente, um novo instantâneo deve ser criado.  
  
    -   Para descartar um artigo de uma publicação, consulte [Adicionar e descartar artigos de uma publicação & #40. SQL Server Management Studio e 41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md) ou [Excluir um artigo](../../../relational-databases/replication/publish/delete-an-article.md).  
  
2.  Após descartar um artigo de uma publicação, é necessário criar um novo instantâneo para a publicação (e todas as partições se for uma publicação de mesclagem com filtros com parâmetros).  
  
    -   Para criar um novo instantâneo, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   Para criar um novo instantâneo para uma publicação de mesclagem com filtros com parâmetros, consulte [criar um instantâneo para uma publicação de mesclagem com filtros com parâmetros](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Como observado anteriormente, em alguns casos, descartar um artigo exige descartar assinaturas, recriá-las e, então, sincronizá-las. Para obter mais informações, consulte [assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md) e [sincronizar dados](../../../relational-databases/replication/synchronize-data.md).  
  
## Consulte também  
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Reinicializar as assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  