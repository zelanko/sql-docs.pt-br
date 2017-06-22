---
title: "Remover um instantâneo de banco de dados (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing database snapshots
- deleting database snapshots
- database snapshots [SQL Server], deleting
ms.assetid: ad70ec97-d5fb-41aa-b72a-915e74b61b76
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9dc2993da01eb4c68f24c4077ea79ff045a8106a
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="drop-a-database-snapshot-transact-sql"></a>Descartar um instantâneo do banco de dados (Transact-SQL)
  A remoção de um instantâneo do banco de dados exclui o instantâneo do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exclui os arquivos esparsos utilizados pelo instantâneo. Quando um instantâneo do banco de dados é removido, todas as conexões de usuário com ele são encerradas.  
  
## <a name="security"></a>Segurança  
  
###  <a name="Permissions"></a> Permissões  
 Qualquer usuário com permissões DROP DATABASE pode remover um instantâneo do banco de dados.  
  
##  <a name="TsqlProcedure"></a> Como remover um instantâneo do banco de dados (usando o Transact-SQL)  
 **Para remover um instantâneo do banco de dados**  
  
1.  Identifique o instantâneo do banco de dados que deseja remover. Você pode exibir os instantâneos em um banco de dados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, veja [Exibir um instantâneo de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md).  
  
2.  Emita uma instrução [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) , especificando o nome do instantâneo do banco de dados ser removido. A sintaxe é a seguinte:  
  
     DROP DATABASE *database_snapshot_name* [ **,**...*n* ]  
  
     Em que *database_snapshot_name* é o nome do instantâneo de banco de dados a ser removido.  
  
####  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Este exemplo remove um instantâneo do banco de dados denominado SalesSnapshot0600 sem afetar o banco de dados de origem.  
  
```  
DROP DATABASE SalesSnapshot0600 ;  
```  
  
 Todas as conexões de usuário para SalesSnapshot0600 são interrompidas, e todos os arquivos esparsos do sistema de arquivos NTFS usados pelo instantâneo são excluídos.  
  
> [!NOTE]  
>  Para obter informações sobre o uso de arquivos esparsos por instantâneos do banco de dados, veja [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Exibir um instantâneo de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [Reverter um banco de dados a um instantâneo do banco de dados](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
  
## <a name="see-also"></a>Consulte também  
 [DROP DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
