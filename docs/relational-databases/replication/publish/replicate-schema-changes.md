---
title: "Replicar altera&#231;&#245;es de esquema | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicação [SQL Server], alterações de esquema"
  - "esquemas [replicação do SQL Server], replicando alterações"
ms.assetid: c09007f0-9374-4f60-956b-8a87670cd043
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# Replicar altera&#231;&#245;es de esquema
  Este tópico descreve como replicar alterações de esquema no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Se você fizer as seguintes alterações de esquema um artigo publicado, elas serão propagadas, por padrão, a todos os Assinantes do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para replicar alterações de esquema usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A instrução ALTER TABLE … DROP COLUMN é sempre replicada para todos os Assinantes cuja assinatura contém as colunas que estão sendo descartadas, mesmo se você desabilitar a replicação de alterações de esquema.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Se você não deseja replicar alterações de esquema para uma publicação, desabilite a replicação das alterações de esquema no **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para desabilitar a replicação de alterações de esquema  
  
1.  No **Opções de assinatura** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, defina o valor da **replicar alterações de esquema** propriedade **False**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Para propagar apenas alterações de esquema específicas, defina a propriedade como **True** antes de uma alteração de esquema e, então, defina-a como **False** depois que a alteração for feita. Por outro lado, para propagar a maioria das alterações de esquema, mas não uma determinada alteração, defina a propriedade como **False** antes da alteração de esquema e, então, defina-a como **True** depois que a alteração for feita.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 Você pode usar procedimentos armazenados de replicação para especificar se estas alterações de esquema serão replicadas. O procedimento armazenado usado depende do tipo de publicação.  
  
#### Para criar um instantâneo ou publicação transacional que não replicam alterações de esquema  
  
1.  No publicador do banco de dados de publicação, execute [sp_addpublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), especificando um valor de **0** para **@replicate_ddl**. Para obter mais informações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### Para criar uma publicação de mesclagem que não reproduz alterações de esquema  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), especificando um valor de **0** para **@replicate_ddl**. Para obter mais informações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### Para desabilitar temporariamente a replicação das alterações de esquema para um instantâneo ou publicação transacional  
  
1.  Para uma publicação com a replicação de alterações de esquema, execute [sp_changepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), especificando um valor de **replicate_ddl** para **@property** e um valor de **0** para **@value**.  
  
2.  Execute o comando DDL no objeto publicado.  
  
3.  (Opcional) Habilitar novamente replicando alterações de esquema executando [sp_changepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), especificando um valor de **replicate_ddl** para **@property** e um valor de **1** para **@value**.  
  
#### Para desabilitar temporariamente a replicação das alterações de esquema para uma publicação de mesclagem  
  
1.  Para uma publicação com a replicação de alterações de esquema, execute [sp_changemergepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), especificando um valor de **replicate_ddl** para **@property** e um valor de **0** para **@value**.  
  
2.  Execute o comando DDL no objeto publicado.  
  
3.  (Opcional) Habilitar novamente replicando alterações de esquema executando [sp_changemergepublication & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), especificando um valor de **replicate_ddl** para **@property** e um valor de **1** para **@value**.  
  
## Consulte também  
 [Fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  