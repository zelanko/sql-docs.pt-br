---
title: "Publicar a execu&#231;&#227;o de um procedimento armazenado em uma publica&#231;&#227;o transacional (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "publicação [replicação do SQL Server], execução de procedimento armazenado"
  - "procedimentos armazenados [replicação do SQL Server], publicação"
ms.assetid: 1d3a3525-0bc5-466f-b097-5359dc74432d
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Publicar a execu&#231;&#227;o de um procedimento armazenado em uma publica&#231;&#227;o transacional (SQL Server Management Studio)
  Especificar que a execução de um procedimento armazenado (em vez de apenas sua definição) deve ser publicada no **Propriedades do artigo - \< artigo>** caixa de diálogo. Essa caixa de diálogo está disponível no Assistente de nova publicação e o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
 A definição do procedimento (instrução CREATE PROCEDURE) será replicada para o Assinante quando a inscrição for inicializada. Quando o procedimento armazenado for executado no Publicador, a replicação executará o procedimento correspondente no Assinante.  
  
### Para publicar a execução de um procedimento armazenado  
  
1.  Sobre o **artigos** página do Assistente de nova publicação ou o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione um procedimento armazenado.  
  
2.  Clique em **Propriedades do artigo**, e, em seguida, clique em **definir propriedades de procedimento armazenado realçado**.  
  
3.  No **Propriedades do artigo - \< artigo>** caixa de diálogo, especifique um dos valores a seguir para o **replicar** opção:  
  
    -   **Execução do procedimento armazenado**  
  
    -   **Execução em uma transação serializável do SP**  
  
         Essa é a opção recomendada, uma vez que ela replica a execução do procedimento apenas se o procedimento for executado dentro do contexto de uma transação serializável. Se o procedimento armazenado for executado fora de uma transação serializável, as alterações dos dados nas tabelas publicadas serão replicadas como uma série de instruções DML (Data Manipulation Language).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
## Consulte também  
 [Publicando execução de procedimento armazenado em replicação transacional](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)  
  
  