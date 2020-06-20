---
title: Exibir as propriedades e o conteúdo de um dispositivo de backup lógico (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
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
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f2bdf41e3dbda079e3627ff7a7c1c3c78103b728
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84956063"
---
# <a name="view-the-properties-and-contents-of-a-logical-backup-device-sql-server"></a>Exibir as propriedades e o conteúdo de um dispositivo de backup lógico (SQL Server)
  Este tópico descreve como exibir as propriedades e o conteúdo de um dispositivo de backup lógico no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir as propriedades e o conteúdo de um dispositivo de backup lógico usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Para obter informações sobre segurança, veja [RESTORE LABELONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql).  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, a obtenção de informações sobre um conjunto ou dispositivo de backup exige a permissão CREATE DATABASE. Para obter mais informações, veja [GRANT Database Permissions &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-permissions-transact-sql).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>Para exibir as propriedades e o conteúdo de um dispositivo de backup lógico  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], em Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
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
>  Para obter mais informações, consulte a [página Conteúdo da Mídia](backup-device-media-contents-page.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>Para exibir as propriedades e o conteúdo de um dispositivo de backup lógico  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Use a instrução [RESTORE LABELONLY](/sql/t-sql/statements/restore-statements-labelonly-transact-sql) . Este exemplo retorna informações sobre o dispositivo de backup lógico `AdvWrks2008R2Backup` .  
  
```sql  
USE AdventureWorks2012 ;  
RESTORE LABELONLY  
   FROM AdvWrks2008R2Backup ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [backupfilegroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfilegroup-transact-sql)   
 [backupfile &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfile-transact-sql)   
 [conjunto de backup &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [backupmediaset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediaset-transact-sql)   
 [backupmediafamily &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediafamily-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [Dispositivos de backup &#40;SQL Server&#41;](backup-devices-sql-server.md)  
  
  
