---
title: "Habilitar um banco de dados para replica&#231;&#227;o (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "bancos de dados [replica&#231;&#227;o do SQL Server]"
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# Habilitar um banco de dados para replica&#231;&#227;o (SQL Server Management Studio)
  Um banco de dados está implicitamente habilitado para replicação quando um membro de **sysadmin** função fixa de servidor cria uma publicação com o novo Assistente de publicação. Um membro do **sysadmin** função fixa de servidor também pode habilitar um banco de dados para replicação explicitamente, para que um membro do **db_owner** função fixa de banco de dados pode criar uma ou mais publicações no banco de dados. Para habilitar um banco de dados explicitamente, use o **bancos de dados de publicação** página o **Propriedades do publicador - \< publicador>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [criar uma publicação](../../relational-databases/replication/publish/create-a-publication.md).  
  
### Para habilitar um banco de dados para replicação  
  
1.  No **bancos de dados de publicação** página do **Propriedades do publicador - \< publicador>** caixa de diálogo, selecione o **transacional** e/ou **Mesclar** caixa de seleção para cada banco de dados que você deseja replicar. Selecione **transacional** para habilitar o replicação de instantâneo no banco de dados.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  