---
title: Renomear um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], renaming
- renaming databases
ms.assetid: 44c69d35-abcb-4da3-9370-5e0bc9a28496
caps.latest.revision: 19
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8d27c37f449d30a95eb56142b71116f6b7548b4a
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43103946"
---
# <a name="rename-a-database"></a>Renomear um banco de dados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como renomear um banco de dados definido pelo usuário no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. O nome do banco de dados pode incluir qualquer caractere que segue as regras para identificadores.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para renomear um banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Follow Up:**  [After renaming a database](#FollowUp)  

> [!NOTE]
> Para renomear um banco de dados no Banco de Dados SQL do Azure, use a instrução [ALTER DATABASE (Banco de Dados SQL do Azure)](../../t-sql/statements/alter-database-azure-sql-database.md). Para renomear um banco de dados no SQL Data Warehouse do Azure ou Parallel Data Warehouse, use a instrução [RENAME (Transact-SQL)](../../t-sql/statements/rename-transact-sql.md).
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Os bancos de dados de sistema não podem ser renomeados.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-rename-a-database"></a>Para renomear um banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e expanda-a.  
  
2.  Certifique-se de que ninguém esteja usando o banco de dados e, em seguida, [defina o banco de dados como modo de usuário único](../../relational-databases/databases/set-a-database-to-single-user-mode.md).  
  
3.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados para renomear e, depois, clique em **Renomear**.  
  
4.  Digite o novo nome do banco de dados e, depois, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-rename-a-database"></a>Para renomear um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo altera o nome do banco de dados `AdventureWorks2012` para `Northwind`.  
  
```sql  
USE master;  
GO  
ALTER DATABASE AdventureWorks2012  
Modify Name = Northwind ;  
GO  
```  
  
###  <a name="TsqlExample"></a>   
##  <a name="FollowUp"></a> Acompanhamento: depois de renomear um banco de dados  
 Faça backup do banco de dados **mestre** e, em seguida, renomeie qualquer banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [Identificadores de banco de dados](../../relational-databases/databases/database-identifiers.md)  
  
  
