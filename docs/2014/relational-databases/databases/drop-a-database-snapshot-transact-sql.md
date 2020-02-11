---
title: Remover um instantâneo de banco de dados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- removing database snapshots
- deleting database snapshots
- database snapshots [SQL Server], deleting
ms.assetid: ad70ec97-d5fb-41aa-b72a-915e74b61b76
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d1387b6321ace59ec8a0c13ed03444553f4adf85
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62871910"
---
# <a name="drop-a-database-snapshot-transact-sql"></a>Descartar um instantâneo do banco de dados (Transact-SQL)
  A remoção de um instantâneo do banco de dados exclui o instantâneo do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exclui os arquivos esparsos utilizados pelo instantâneo. Quando um instantâneo do banco de dados é removido, todas as conexões de usuário com ele são encerradas.  
  
## <a name="security"></a>Segurança  
  
###  <a name="Permissions"></a> Permissões  
 Qualquer usuário com permissões DROP DATABASE pode remover um instantâneo do banco de dados.  
  
##  <a name="TsqlProcedure"></a> Como remover um instantâneo do banco de dados (usando o Transact-SQL)  
 **Para remover um instantâneo do banco de dados**  
  
1.  Identifique o instantâneo do banco de dados que deseja remover. Você pode exibir os instantâneos em um banco de dados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações, veja [Exibir um instantâneo de banco de dados &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md).  
  
2.  Emita uma instrução [DROP DATABASE](/sql/t-sql/statements/drop-database-audit-specification-transact-sql) , especificando o nome do instantâneo do banco de dados ser removido. A sintaxe é mostrada a seguir:  
  
     DROP DATABASE *database_snapshot_name* [ **,** ...*n* ]  
  
     Em que *database_snapshot_name* é o nome do instantâneo de banco de dados a ser removido.  
  
####  <a name="TsqlExample"></a> Exemplo (Transact-SQL)  
 Este exemplo remove um instantâneo do banco de dados denominado SalesSnapshot0600 sem afetar o banco de dados de origem.  
  
```  
DROP DATABASE SalesSnapshot0600 ;  
```  
  
 Todas as conexões de usuário para SalesSnapshot0600 são interrompidas, e todos os arquivos esparsos do sistema de arquivos NTFS usados pelo instantâneo são excluídos.  
  
> [!NOTE]  
>  Para obter informações sobre o uso de arquivos esparsos por instantâneos do banco de dados, veja [Instantâneos de banco de dados &#40;SQL Server&#41;](database-snapshots-sql-server.md).  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um instantâneo de banco de dados &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [Exibir um instantâneo de banco de dados &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)  
  
-   [Reverter um banco de dados para um instantâneo do banco de dados](revert-a-database-to-a-database-snapshot.md)  
  

  
## <a name="see-also"></a>Consulte Também  
 [DROP DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)   
 [Instantâneos de banco de dados &#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
