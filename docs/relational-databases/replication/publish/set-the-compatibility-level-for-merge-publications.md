---
title: "Definir o nível de compatibilidade para publicações de mesclagem | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [SQL Server], replication
- backward compatibility [SQL Server], replication
- publications [SQL Server replication], backward compatibility
ms.assetid: db47ac73-948b-4d77-b272-bb3565135ea5
caps.latest.revision: 33
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 99a56af259a4be7f07183f22874385b515d6c044
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="set-the-compatibility-level-for-merge-publications"></a>Definir o nível de compatibilidade para publicações de mesclagem
  Este tópico descreve como definir o nível de compatibilidade de publicações de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. A replicação de mesclagem usa o nível de compatibilidade da publicação para determinar quais recursos podem ser usados pelas publicações em um determinado banco de dados.  
  
 **Neste tópico**  
  
-   **Para definir o nível de compatibilidade para publicações de mesclagem, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Defina o nível de compatibilidade na página **Tipos de Assinante** do Assistente para Nova Publicação. Para obter mais informações sobre como acessar esse assistente, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md). Depois da criação de um instantâneo de publicação, é possível aumentar mas não diminuir o nível de compatibilidade. Aumente o nível de compatibilidade na página **Geral** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Se você aumentar o nível de compatibilidade da publicação, quaisquer assinaturas existentes nos servidores que executem versões anteriores ao nível de compatibilidade não conseguirão sincronizar.  
  
> [!NOTE]  
>  Como o nível de compatibilidade tem implicações para outras propriedades da publicação e para a definição de quais propriedades de artigo são válidas, não altere o nível de compatibilidade e outras propriedades no mesmo uso da caixa de diálogo. O instantâneo porque a publicação deveria ser regenerada depois que a propriedade seja alterada.  
  
#### <a name="to-set-the-publication-compatibility-level"></a>Para definir o nível de compatibilidade de publicação  
  
-   Na página **Tipos de Assinante** do Assistente para Nova Publicação, selecione os tipos de Assinantes para os quais a publicação deve fornecer suporte.  
  
#### <a name="to-increase-the-publication-compatibility-level"></a>Para aumentar o nível de compatibilidade de publicação  
  
-   Na página **Geral** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**, selecione **Nível de compatibilidade**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
 O nível de compatibilidade para uma publicação de mesclagem, pode ser definida, programaticamente, quando uma publicação é criada ou modificada programaticamente depois. Você pode usar procedimentos armazenados de replicação para definir ou alterar esta propriedade de publicação.  
  
#### <a name="to-set-the-publication-compatibility-level-for-a-merge-publication"></a>Para definir o nível de compatibilidade para uma publicação de mesclagem  
  
1.  No Publicador, execute [sp_addmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), especificando um valor para **@publication_compatibility_level** para tornar a publicação compatível com versões antigas de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
#### <a name="to-change-the-publication-compatibility-level-of-a-merge-publication"></a>Para definir o nível de compatibilidade da publicação de uma publicação de mesclagem  
  
1.  Execute [sp_changemergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), especificando **publication_compatibility_level** para **@property** e o nível de compatibilidade da publicação adequada para **@value**.  
  
#### <a name="to-determine-the-publication-compatibility-level-of-a-merge-publication"></a>Para determinar o nível de compatibilidade da publicação de uma publicação de mesclagem  
  
1.  Execute [sp_helpmergepublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando a publicação desejada.  
  
2.  Localize o nível de compatibilidade da publicação na coluna **backward_comp_level** no conjunto de resultados.  
  
###  <a name="TsqlExample"></a> Exemplos (Transact-SQL)  
 Esse exemplo cria uma publicação de mesclagem e define o nível de compatibilidade da publicação.  
  
```  
-- To avoid storing the login and password in the script file, the values   
-- are passed into SQLCMD as scripting variables. For information about   
-- how to use scripting variables on the command line and in SQL Server  
-- Management Studio, see the "Executing Replication Scripts" section in  
-- the topic "Programming Replication Using System Stored Procedures".  
  
--Add a new merge publication.  
DECLARE @publicationDB AS sysname;  
DECLARE @publication AS sysname;  
DECLARE @login AS sysname;  
DECLARE @password AS sysname;  
SET @publicationDB = N'AdventureWorks2012';   
SET @publication = N'AdvWorksSalesOrdersMerge'   
SET @login = $(Login);  
SET @password = $(Password);  
  
-- Create a new merge publication.   
USE [AdventureWorks2012]  
EXEC sp_addmergepublication   
@publication = @publication,   
-- Set the compatibility level to SQL Server 2014.  
@publication_compatibility_level = '120RTM';   
  
-- Create the snapshot job for the publication.  
EXEC sp_addpublication_snapshot   
@publication = @publication,  
@job_login = @login,  
@job_password = @password;  
GO  
```  
  
 Esse exemplo altera uma publicação de mesclagem e define o nível de compatibilidade da publicação.  
  
> [!NOTE]  
>  Alterar o nível de compatibilidade da publicação pode não ser permitido se a publicação usar qualquer recurso que necessite de um nível de compatibilidade específico. Para obter mais informações, consulte [Compatibilidade com versões anteriores de replicação](../../../relational-databases/replication/replication-backward-compatibility.md).  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
  
-- Change the publication compatibility level to   
-- SQL Server 2012.  
EXEC sp_changemergepublication   
@publication = @publication,   
@property = N'publication_compatibility_level',   
@value = N'110RTM';  
GO  
  
```  
  
 Esse exemplo retorna o nível de compatibilidade da publicação atual para a publicação de mesclagem.  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
EXEC sp_helpmergepublication   
@publication = @publication;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
  
