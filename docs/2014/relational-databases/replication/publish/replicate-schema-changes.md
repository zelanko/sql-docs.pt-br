---
title: Replicar alterações de esquema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: c09007f0-9374-4f60-956b-8a87670cd043
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84918dd3f50d129485911fc880e67c0152fa905c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73882241"
---
# <a name="replicate-schema-changes"></a>Replicar alterações de esquema
  Este tópico descreve como replicar alterações de esquema no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Se você fizer as seguintes alterações de esquema em um artigo publicado, elas serão propagadas, por padrão [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , para os assinantes:  
  
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
  
-   A instrução ALTER TABLE... A instrução DROP COLUMN sempre é replicada para todos os assinantes cuja assinatura contém as colunas que estão sendo descartadas, mesmo se você desabilitar a replicação de alterações de esquema.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Se você não deseja replicar as alterações de esquema de uma publicação, desabilite a replicação de alterações de esquema na caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-disable-replication-of-schema-changes"></a>Para desabilitar a replicação de alterações de esquema  
  
1.  Na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**, defina o valor da propriedade **Replicar alterações de esquema** como **False**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Para propagar apenas alterações de esquema específicas, defina a propriedade como **True** antes de uma alteração de esquema e, então, defina-a como **False** depois que a alteração for feita. Por outro lado, para propagar a maioria das alterações de esquema, mas não uma determinada alteração, defina a propriedade como **False** antes da alteração de esquema e, então, defina-a como **True** depois que a alteração for feita.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Você pode usar procedimentos armazenados de replicação para especificar se estas alterações de esquema serão replicadas. O procedimento armazenado usado depende do tipo de publicação.  
  
#### <a name="to-create-a-snapshot-or-transactional-publication-that-does-not-replicate-schema-changes"></a>Para criar um instantâneo ou publicação transacional que não replicam alterações de esquema  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addpublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql), especificando um valor de **0** para ** \@replicate_ddl**. Para obter mais informações, consulte [Criar uma assinatura](create-a-publication.md).  
  
#### <a name="to-create-a-merge-publication-that-does-not-replicate-schema-changes"></a>Para criar uma publicação de mesclagem que não reproduz alterações de esquema  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql), especificando um valor de **0** para ** \@replicate_ddl**. Para obter mais informações, consulte [Criar uma assinatura](create-a-publication.md).  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-snapshot-or-transactional-publication"></a>Para desabilitar temporariamente a replicação das alterações de esquema para um instantâneo ou publicação transacional  
  
1.  Para uma publicação com replicação de alterações de esquema, execute [sp_changepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando um valor **de replicate_ddl** para ** \@Propriedade** e um valor de **0** para ** \@valor**.  
  
2.  Execute o comando DDL no objeto publicado.  
  
3.  Adicional Habilite novamente a replicação de alterações de esquema executando [sp_changepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), especificando um valor **de replicate_ddl** para ** \@Propriedade** e um valor de **1** para ** \@valor**.  
  
#### <a name="to-temporarily-disable-replicating-schema-changes-for-a-merge-publication"></a>Para desabilitar temporariamente a replicação das alterações de esquema para uma publicação de mesclagem  
  
1.  Para uma publicação com replicação de alterações de esquema, execute [sp_changemergepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando um valor **de replicate_ddl** para ** \@Propriedade** e um valor de **0** para ** \@valor**.  
  
2.  Execute o comando DDL no objeto publicado.  
  
3.  Adicional Habilite novamente a replicação de alterações de esquema executando [sp_changemergepublication &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), especificando um valor **de replicate_ddl** para ** \@Propriedade** e um valor de **1** para ** \@valor**.  
  
## <a name="see-also"></a>Consulte Também  
 [Fazer alterações de esquema em bancos de dados de publicação](make-schema-changes-on-publication-databases.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](make-schema-changes-on-publication-databases.md)  
  
  
