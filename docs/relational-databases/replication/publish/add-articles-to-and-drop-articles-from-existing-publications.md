---
title: "Adicionar e remover artigos de publicações existentes | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], dropping
- deleting articles
- removing articles
- dropping articles
- adding articles
- administering replication, articles
- publications [SQL Server replication], adding and dropping articles
- articles [SQL Server replication], adding
ms.assetid: b148e907-e1f2-483b-bdb2-59ea596efceb
caps.latest.revision: "48"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 082b20b502afb8201ab63db204bf0fff25e17c66
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="add-articles-to-and-drop-articles-from-existing-publications"></a>Adicionar e remover artigos de publicações existentes
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Depois que uma publicação é criada, é possível adicionar e remover artigos. Os artigos podem ser adicionados a qualquer hora, mas as ações necessárias para descartar artigos dependem do tipo de replicação e de quando o artigo é descartado.  
  
## <a name="adding-articles"></a>adicionando artigos  
 Adicionar um artigo envolve: adicionar o artigo à publicação; criar um novo instantâneo para a publicação; sincronizar a assinatura para aplicar o esquema e os dados para o novo artigo.  
  
> [!NOTE]  
>  Se você adicionar um artigo a uma publicação de mesclagem e o artigo existente depender do artigo novo, será preciso especificar uma ordem de processamento para ambos os artigos usando o parâmetro **@processing_order** de [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) e [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Considere o seguinte cenário: uma tabela é publicada, mas não é publicada a função que é referenciada pela tabela. Se a função não for publicada, a tabela não poderá ser criada no Assinante. Ao adicionar a função à publicação: especifique o valor **1** para o parâmetro **@processing_order** de **sp_addmergearticle**e especifique o valor **2** para o parâmetro **@processing_order** de **sp_changemergearticle**, especificando o nome da tabela para o parâmetro **@article**. Essa ordem de processamento garante a criação da função no Assinante antes da tabela que depende disso. É possível usar números diferentes para cada artigo, desde que o número para a função seja menor que o número para a tabela.  
  
1.  Adicione um ou mais artigos com um dos métodos seguintes:  
  
    -   [Adicionar e remover artigos em uma publicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)  
  
    -   [Definir um Artigo](../../../relational-databases/replication/publish/define-an-article.md)  
  
2.  Após adicionar um artigo a uma publicação, é necessário criar um novo instantâneo para a publicação (e todas as partições se for uma publicação de mesclagem com filtros com parâmetros). O Agente de Distribuição ou o Agente de Mesclagem então copiará o esquema e os dados para o novo artigo para o Assinante (ele não reinicializa a publicação inteira).  
  
    -   Para criar um novo instantâneo, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   Para criar um novo instantâneo para uma publicação de mesclagem com filtros com parâmetros, consulte [Criar um instantâneo pra publicação de mesclagem com filtros com parâmetros](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
3.  Depois que o instantâneo é criado, sincronize a assinatura para copiar o esquema e os dados para o novo artigo.  
  
    -   Para sincronizar uma assinatura push, consulte [Sincronizar uma assinatura push](../../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
    -   Para sincronizar uma assinatura pull, consulte [Sincronizar uma assinatura pull](../../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
## <a name="dropping-articles"></a>descartando artigos  
 Os artigos podem ser descartados de uma publicação a qualquer hora, mas é necessário levar em conta os seguintes comportamentos:  
  
-   Descartar um artigo de uma publicação não remove o objeto do banco de dados de publicação ou o objeto correspondente do banco de dados de assinatura. Use DROP \<Objeto> para remover esses objetos, se necessário. Ao remover um artigo relacionado a outros artigos publicados por meio de restrições de chave estrangeira, recomendamos remover manualmente a tabela no Assinante ou usando uma execução de script sob demanda: especifique o script que inclua as instruções DROP \<Objeto> apropriadas. Para obter mais informações, consulte [Executar scripts durante a sincronização &#40;Programação do Transact-SQL de Replicação&#41;](../../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md).  
  
-   Para publicações de mesclagem com nível de compatibilidade 90RTM ou superior, os artigos podem ser descartados a qualquer hora, porém um novo instantâneo é requerido. Adicionalmente:  
  
    -   Se o artigo é um artigo pai em um filtro de junção ou relação de registro lógico, as relações devem ser descartadas primeiro, o que requer a reinicialização.  
  
    -   Se o artigo tiver o último filtro com parâmetros em uma publicação, as assinaturas deverão ser reinicializadas.  
  
-   Para publicações de mesclagem com nível de compatibilidade inferior a 90RTM, os artigos podem ser descartados sem considerações especiais anteriores à sincronização inicial de assinaturas. Se o artigo for descartado depois que uma ou mais assinaturas forem sincronizadas, as assinaturas devem ser descartadas, recriadas e sincronizadas.  
  
-   Para publicações de instantâneo ou publicações transacionais, os artigos podem ser descartados sem considerações especiais antes de as assinatura serem criadas. Se o artigo for descartado depois que uma ou mais assinaturas forem criadas, as assinaturas devem ser descartadas, recriadas e sincronizadas. Para obter mais informações sobre como remover assinaturas, consulte [Assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md) e [sp_dropsubscription &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md). **sp_dropsubscription** permite a você remover um único artigo da assinatura, em vez da assinatura inteira.  
  
1.  Descartar um artigo de uma publicação envolve descartar o artigo e criar um novo instantâneo para a publicação. Descartar um artigo invalida o instantâneo atual; consequentemente, um novo instantâneo deve ser criado.  
  
    -   Para remover um artigo de uma publicação, consulte [Adicionar e remover artigos de uma publicação &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md) ou [Excluir um artigo](../../../relational-databases/replication/publish/delete-an-article.md).  
  
2.  Após descartar um artigo de uma publicação, é necessário criar um novo instantâneo para a publicação (e todas as partições se for uma publicação de mesclagem com filtros com parâmetros).  
  
    -   Para criar um novo instantâneo, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
    -   Para criar um novo instantâneo para uma publicação de mesclagem com filtros com parâmetros, consulte [Criar um instantâneo pra publicação de mesclagem com filtros com parâmetros](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Como observado anteriormente, em alguns casos, descartar um artigo exige descartar assinaturas, recriá-las e, então, sincronizá-las. Para obter mais informações, consulte [Assinar publicações](../../../relational-databases/replication/subscribe-to-publications.md) e [Sincronizar dados](../../../relational-databases/replication/synchronize-data.md).  
 
 > [!NOTE]
 > **[!INCLUDE[ssSQL15](../../../includes/sssql14-md.md)] Service Pack 2** ou superior e **[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] Service Pack 1** ou superior dão suporte a remover tabelas usando o comando DLL **DROP TABLE** para artigos que participam da Replicação Transacional. Se a publicação der suporte para DROP TABLE DDL, a operação de DROP TABLE removerá a tabela da publicação e do banco de dados. O agente do leitor de log lançará um comando de limpeza para o banco de dados de distribuição da tabela removida e fará a limpeza dos metadados do publicador. Se o leitor de log não tiver processado todos os registros de log que fazem referência à tabela removida, ele ignorará novos comandos associados à tabela removida. Registros já processados serão entregues ao banco de dados de distribuição. Eles poderão ser aplicados ao banco de dados do Assinante se o Agente de Distribuição processá-los antes que o Leitor de Log limpar os artigos obsoletos (removidos). A configuração **padrão** para todas as publicações de replicação transacional é não dar suporte a DLL de DROP TABLE. O artigo [KB 3170123](https://support.microsoft.com/en-us/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1) apresenta mais detalhes sobre essa melhoria.

  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Reinicializar as assinaturas](../../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  
