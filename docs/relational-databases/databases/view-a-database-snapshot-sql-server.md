---
title: Exibir um instantâneo de banco de dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], viewing
- displaying database snapshots
- viewing database snapshots
ms.assetid: 123f19b2-0850-4033-8507-59ebdfb368ee
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5f09f279c82a9fb28e259951be2bf78f9ca93aae
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907907"
---
# <a name="view-a-database-snapshot-sql-server"></a>Exibir um instantâneo de banco de dados (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
3.  Para listar os instantâneos do banco de dados da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte a coluna **source_database_id** da exibição do catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) para obter valores não nulos.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [Reverter um banco de dados a um instantâneo do banco de dados](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
-   [Remover um instantâneo do banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
