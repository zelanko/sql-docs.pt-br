---
title: "Exibir as propriedades e o conteúdo de um dispositivo de backup lógico (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying backup content
- viewing backup content
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
- backing up databases [SQL Server], properties
- displaying backup properties
- backup devices [SQL Server], viewing information
- viewing backup properties
- database backups [SQL Server], properties
ms.assetid: 3a309074-e816-454d-b6c3-fcfdde0cbf74
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 332fbe8c9b624e1ca48562236aa09229f21657c8
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="view-the-properties-and-contents-of-a-logical-backup-device-sql-server"></a>Exibir as propriedades e o conteúdo de um dispositivo de backup lógico (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como exibir as propriedades e o conteúdo de um dispositivo de backup lógico no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir as propriedades e o conteúdo de um dispositivo de backup lógico usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações sobre segurança, veja [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md).  
  
####  <a name="Permissions"></a> Permissões  
 No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, a obtenção de informações sobre um conjunto ou dispositivo de backup exige a permissão CREATE DATABASE. Para obter mais informações, veja [GRANT Database Permissions &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>Para exibir as propriedades e o conteúdo de um dispositivo de backup lógico  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Objetos de Servidor**e expanda **Dispositivos de Backup**.  
  
3.  Clique no dispositivo e clique com o botão direito do mouse em **Propriedades**, isso abre a caixa de diálogo **Dispositivo de Backup** .  
  
4.  A página **Geral** exibe o nome de dispositivo e destino que são um dispositivo de fita ou um caminho de arquivo.  
  
5.  No painel **Selecionar uma Página** , clique em **Conteúdo da Mídia**.  
  
6.  O painel à direita exibe os seguintes painéis de propriedades:  
  
    -   **Mídia**  
  
         Informações de sequência de mídia (o número de sequência de mídia, o número de sequência da família e o identificador de espelho, se houver) e a data e hora de criação da mídia.  
  
    -   **Conjunto de mídias**  
  
         Informações do conjunto de mídias: nome e descrição do conjunto de mídias, se houver, e o número de famílias no conjunto de mídias.  
  
7.  A grade **Conjuntos de backups** exibe informações sobre o conteúdo do conjunto de mídias.  
  
> [!NOTE]  
>  Para obter mais informações, consulte a [página Conteúdo da Mídia](../../relational-databases/backup-restore/backup-device-media-contents-page.md).  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>Para exibir as propriedades e o conteúdo de um dispositivo de backup lógico  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Use a instrução [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) . Este exemplo retorna informações sobre o dispositivo de backup lógico `AdvWrks2008R2Backup` .  
  
```sql  
USE AdventureWorks2012 ;  
RESTORE LABELONLY  
   FROM AdvWrks2008R2Backup ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [Dispositivos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
