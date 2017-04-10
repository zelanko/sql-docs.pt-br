---
title: "Propriedades de Publica&#231;&#227;o, Parti&#231;&#245;es de Dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.pubproperties.datapartitions.f1"
ms.assetid: 5869edb7-d05f-495b-b828-b7fd5e828d20
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Propriedades de Publica&#231;&#227;o, Parti&#231;&#245;es de Dados
  A página **Partições de Dados** da caixa de diálogo **Propriedades de Publicação** permite definir partições de dados para publicações de mesclagem que usam filtragem com parâmetros. Depois de definir as partições, você pode gerar instantâneos para essas partições, fornecendo conjuntos de dados iniciais diferentes para Assinantes diferentes, com base nas propriedades de conexão (logon e/ou nome de computador) dos Assinantes. Você pode também selecionar para permitir aos Assinantes solicitarem a entrega e a geração de instantâneo, se não tiverem um instantâneo disponível para a partição, na primeira vez em que sincronizarem. Para obter mais informações, consulte [Create a Snapshot for a Merge Publication with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
## Opções  
 **Adicionar**  
 Clique em **Add** para definir uma partição. Na **Adicionar partição de dados** caixa de diálogo, especifique valores para **HOST_NAME ()** e/ou **suser_sname ()**, e definir um agendamento de atualização de instantâneos.  
  
 **Editar**  
 Selecione uma partição existente na grade e clique em **Editar** para editar a partição.  
  
 **Delete (excluir)**  
 Selecione uma partição existente na grade e clique em **Excluir** para excluir a partição.  
  
 **Gerar os instantâneos selecionados agora**  
 Selecione uma ou mais partições na grade e clique em **gerar os instantâneos selecionados agora** para gerar instantâneos para essas partições.  
  
 **Limpar os instantâneos existentes**  
 Selecione uma ou mais partições na grade e clique em **Limpar os instantâneos existentes** para limpar os instantâneos para essas partições.  
  
 **Definir automaticamente uma partição e gerar um instantâneo, se necessário, quando um novo Assinante tentar sincronizar**  
 Selecione essa opção se quiser permitir que os Assinantes solicitem geração e aplicação de  instantâneo. Os Assinantes podem exigir essa opção, se não tiverem um instantâneo disponível para a partição, na primeira vez em que sincronizarem.  
  
## Consulte também  
 [Crie uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Visualizar e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-row-filters.md)   
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Instantâneos para publicações de mesclagem com filtros com parâmetros](../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md)  
  
  