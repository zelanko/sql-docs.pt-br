---
title: Exibir um instantâneo de banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], viewing
- displaying database snapshots
- viewing database snapshots
ms.assetid: 123f19b2-0850-4033-8507-59ebdfb368ee
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: df4ba0cc720cd7dd98addff076c1400747da3551
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37188623"
---
# <a name="view-a-database-snapshot-sql-server"></a>Exibir um instantâneo de banco de dados (SQL Server)
  Este tópico explica como exibir um instantâneo do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  Para criar, reverter ou excluir um instantâneo do banco de dados, você deve usar o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Para exibir um instantâneo do banco de dados, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para exibir um instantâneo do banco de dados**  
  
1.  No Pesquisador de Objetos, conecte-se à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda essa instância.  
  
2.  Expandir os **Bancos de Dados**.  
  
3.  Expanda o **Instantâneo do Banco de Dados**e selecione o instantâneo que você quer exibir.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para exibir um instantâneo do banco de dados**  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Para listar os instantâneos do banco de dados da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte a coluna **source_database_id** da exibição do catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) para obter valores não nulos.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um instantâneo de banco de dados &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [Reverter um banco de dados para um instantâneo do banco de dados](revert-a-database-to-a-database-snapshot.md)  
  
-   [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Consulte também  
 [Instantâneos de banco de dados &#40;SQL Server&#41;](database-snapshots-sql-server.md)  
  
  
