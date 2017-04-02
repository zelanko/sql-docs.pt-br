---
title: "Habilitar um Publicador remoto em um Distribuidor (SQL Server Management Studio) | Microsoft Docs"
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
  - "Distribuidores remotos [replicação do SQL Server]"
  - "Publicadores [replicação do SQL Server]"
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# Habilitar um Publicador remoto em um Distribuidor (SQL Server Management Studio)
  Habilite um Publicador a usar um Distribuidor remoto na página **Publicadores** . Esta página está disponível no Assistente para configurar distribuição e o **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Configurar publicação e distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md) e [Exibir e modificar o distribuidor e propriedades do publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### Para habilitar um Publicador no Assistente para Configurar Distribuição  
  
1.  Na página **Publicadores** do Assistente para Configurar Distribuição, clique em **Adicionar**.  
  
2.  Clique em **Adicionar Editor SQL Server**. Para obter informações sobre como habilitar um Oracle Publisher para usar um Distribuidor, consulte [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , especifique a informação de conexão para o Publicador que usará o Distribuidor remoto e, então, clique em **Conectar**.  
  
4.  No **senha do distribuidor** página, o **senha** e **Confirmar senha** caixas de texto, especifique uma senha forte para a **distributor_admin** conta, que a replicação usa para conectar-se do publicador ao distribuidor para executar tarefas administrativas.  
  
5.  Para exibir e modificar as configurações para um editor, clique no botão Propriedades (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### Para habilitar um Publicador na caixa de diálogo Propriedades de Distribuidor  
  
1.  No **editores** página o **Propriedades do distribuidor - \< distribuidor>** caixa de diálogo, clique em **Adicionar**.  
  
2.  Clique em **Adicionar Editor SQL Server**. Para obter informações sobre como habilitar um Oracle Publisher para usar um Distribuidor, consulte [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md).  
  
3.  Na caixa de diálogo **Conectar ao Servidor** , especifique a informação de conexão para o Publicador que usará o Distribuidor remoto e, então, clique em **Conectar**.  
  
4.  No **editores** página, o **senha** e **Confirmar senha** caixas de texto, especifique uma senha forte para a **distributor_admin** conta, que a replicação usa para conectar-se do publicador ao distribuidor para executar tarefas administrativas.  
  
5.  Para exibir e modificar as configurações para um editor, clique no botão Propriedades (**...**).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Consulte também  
 [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Configurar a distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Proteger o distribuidor](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  