---
title: Exibir os dados e arquivos de log em um conjunto de backup (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], viewing backup sets
- viewing backup set information
- backup sets [SQL Server], viewing files in
- displaying backup set information
- transaction log backups [SQL Server], viewing backup sets
- backing up [SQL Server], viewing backup sets
ms.assetid: abb6420c-f809-426e-aeb4-d0a74989cf39
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fe58874e0046a53a33d0580c4477ac89f6cd6e18
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875048"
---
# <a name="view-the-data-and-log-files-in-a-backup-set-sql-server"></a>Exibir os dados e arquivos de log em um conjunto de backup (SQL Server)
  Este tópico descreve como exibir os arquivos de dados e logs em um conjunto de backup no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir os dados e arquivos de log em um conjunto de backup, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações sobre segurança, veja [RESTORE FILELISTONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)  
  
####  <a name="Permissions"></a> Permissões  
 No [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e em versões posteriores, a obtenção de informações sobre um conjunto ou dispositivo de backup exige a permissão CREATE DATABASE. Para obter mais informações, veja [GRANT Database Permissions &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-permissions-transact-sql).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-data-and-log-files-in-a-backup-set"></a>Para exibir os dados e arquivos de log em um conjunto de backup  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados e clique em **Propriedades**, o que abrirá a caixa de diálogo **Propriedades do Banco de Dados** .  
  
4.  No painel **Selecionar uma Página** , clique em **Arquivos**.  
  
5.  Procure na grade **Arquivos de banco de dados** para obter uma lista dos dados e arquivos de log e suas propriedades.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-the-data-and-log-files-in-a-backup-set"></a>Para exibir os dados e arquivos de log em um conjunto de backup  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Use a instrução [RESTORE FILELISTONLY](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql) . Este exemplo retorna informações sobre o segundo conjunto de backup (`FILE=2`) no dispositivo de backup do `AdventureWorksBackups` .  
  
```sql  
USE AdventureWorks2012 ;  
RESTORE FILELISTONLY FROM AdventureWorksBackups   
   WITH FILE=2;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [backupfilegroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfilegroup-transact-sql)   
 [backupfile &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfile-transact-sql)   
 [conjunto de backup &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [backupmediaset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediaset-transact-sql)   
 [backupmediafamily &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediafamily-transact-sql)   
 [Dispositivos de backup &#40;SQL Server&#41;](backup-devices-sql-server.md)  
  
  
