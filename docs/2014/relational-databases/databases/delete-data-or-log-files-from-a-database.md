---
title: Excluir arquivos de dados ou de log de um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], files
- deleting files
- removing files
- removing data
- data deletions [SQL Server]
- file deletion [SQL Server]
- deleting data
ms.assetid: 0db4018c-ce2c-4ba1-bb29-1e4f3791c925
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e0f2de1f7003e61dbdc8e82f7a9b549fd42c77fc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52783428"
---
# <a name="delete-data-or-log-files-from-a-database"></a>Excluir arquivos de dados ou de log de um banco de dados
  Este tópico descreve como excluir arquivos de dados ou de log no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
  
-   Um arquivo deve estar vazio antes que possa ser excluído. Para saber mais, veja [Reduzir um arquivo](shrink-a-file.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-data-or-log-files-from-a-database"></a>Para excluir arquivos de dados ou de log de um banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados do qual deseja excluir o arquivo e depois clique em **Propriedades**.  
  
3.  Selecione a página **Arquivos** .  
  
4.  Na grade **Arquivos de bancos de dados** , selecione o arquivo a ser excluído e, depois, clique em **Remover**.  
  
5.  Clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-delete-data-or-log-files-from-a-database"></a>Para excluir arquivos de dados ou de log de um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo remove o arquivo `test1dat4`.  
  
 [!code-sql[DatabaseDDL#AlterDatabase4](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase4)]  
  
 Para obter mais exemplos, consulte [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).  
  
## <a name="see-also"></a>Consulte também  
 [Reduzir um banco de dados](shrink-a-database.md)   
 [Adicionar arquivos de dados ou de log a um banco de dados](add-data-or-log-files-to-a-database.md)  
  
  
