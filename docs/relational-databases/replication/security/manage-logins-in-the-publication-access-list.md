---
title: "Gerenciar logons na lista de acesso &#224; publica&#231;&#227;o | Microsoft Docs"
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
  - "logons [replicação do SQL Server], lista de acesso da publicação"
  - "publicações [replicação do SQL Server], listas de acesso da publicação"
  - "lista de acesso à publicação (PAL)"
  - "PAL (publication access list)"
  - "logons [replicação do SQL Server], gerenciamento"
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Gerenciar logons na lista de acesso &#224; publica&#231;&#227;o
  Este tópico descreve como gerenciar logons na Lista de Acesso à Publicação no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O acesso a uma publicação é controlado pela PAL (lista de acesso à publicação). É possível adicionar e remover logons e grupos do PAL.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Pré-requisitos](#Prerequisites)  
  
-   **Para gerenciar logons na Lista de Acesso à Publicação, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Você deve associar o logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com um usuário de banco de dados no banco de dados de publicação antes de adicionar o logon à PAL.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Use a lista de acesso da publicação (PAL) no **lista de acesso da publicação** página do **Propriedades de publicação - \< publicação>** caixa de diálogo para gerenciar logons. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para gerenciar logons na PAL  
  
1.  No **lista de acesso da publicação** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, use o **Adicionar**, **Remover**, e **Remover tudo** botões para adicionar e remover logons e grupos da PAL. Não remova **distributor_admin** da PAL. Essa conta é usada para replicação.  
  
    > [!NOTE]  
    >  Se for usado um Distribuidor remoto, as contas da PAL precisarão estar disponíveis tanto no Publicador quanto no Distribuidor. A conta ou deve ser uma conta de domínio ou uma conta local que é definida em ambos os servidores. As senhas associadas a ambos os logons devem ser as mesmas.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para exibir grupos e logons que pertencem à PAL  
  
1.  No publicador do banco de dados de publicação, execute [sp_help_publication_access](../../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md). Para **@publication**, especifique o nome da publicação. Isso exibe informações sobre os grupos e logons na PAL.  
  
#### Para adicionar grupos e logons à PAL  
  
1.  No publicador do banco de dados de publicação, execute [sp_grant_publication_access](../../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md). Para **@publication**especifique o nome da publicação e para **@login**especifique o nome do logon ou grupo que está sendo adicionado.  
  
#### Para remover grupos e logons da PAL  
  
1.  No publicador do banco de dados de publicação, execute [sp_revoke_publication_access](../../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md). Para **@publication**especifique o nome da publicação e para **@login**especifique o nome do logon ou grupo que está sendo removido.  
  
## Consulte também  
 [Manage Logins in the Publication Access List](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)   
 [Modelo de segurança do agente de replicação](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Proteger uma topologia de replicação](../../../relational-databases/replication/security/secure-a-replication-topology.md)   
 [Proteger o Publicador](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  