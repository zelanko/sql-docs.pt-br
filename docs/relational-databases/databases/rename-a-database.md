---
title: Renomear um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], renaming
- renaming databases
ms.assetid: 44c69d35-abcb-4da3-9370-5e0bc9a28496
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a2cfe01b4df32e0966084866a67cea4bfd57bc11
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72907425"
---
# <a name="rename-a-database"></a>Renomear um banco de dados

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como renomear um banco de dados definido pelo usuário em [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ou no Banco de Dados SQL do Azure usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]. O nome do banco de dados pode incluir qualquer caractere que segue as regras para identificadores.  
  
## <a name="in-this-topic"></a>Neste tópico
  
- Antes de começar:  
  
     [Limitações e restrições](#limitations-and-restrictions)  
  
     [Segurança](#security)  
  
- Para renomear um banco de dados usando:  
  
     [SQL Server Management Studio](#rename-a-database-using-sql-server-management-studio)  
  
     [Transact-SQL](#rename-a-database-using-transact-sql)  
  
- **Acompanhamento:**  [Após renomear um banco de dados](#backup-after-renaming-a-database)  

> [!NOTE]
> Para renomear um banco de dados no SQL Data Warehouse do Azure ou Parallel Data Warehouse, use a instrução [RENAME (Transact-SQL)](../../t-sql/statements/rename-transact-sql.md).
  
## <a name="before-you-begin"></a>Antes de começar
  
### <a name="limitations-and-restrictions"></a>Limitações e Restrições  
  
- Os bancos de dados de sistema não podem ser renomeados.
- O nome do banco de dados não pode ser alterado enquanto outros usuários estão acessando o banco de dados. 
  - No SQL Server, você pode definir um banco de dados no modo de usuário único para fechar todas as conexões abertas. Para obter mais informações, veja [definir um banco de dados como modo de usuário único](../../relational-databases/databases/set-a-database-to-single-user-mode.md).
  - No Banco de Dados SQL do Azure, verifique se nenhum outro usuário tem uma conexão aberta ao banco de dados a ser renomeado.
  
### <a name="security"></a>Segurança  
  
#### <a name="permissions"></a>Permissões

Requer a permissão ALTER no banco de dados.  
  
## <a name="rename-a-database-using-sql-server-management-studio"></a>Renomear um banco de dados usando o SQL Server Management Studio

Use as etapas a seguir para renomear um SQL Server ou Banco de Dados SQL do Azure usando o SQL Server Management Studio.

  
1. No **Pesquisador de Objetos**, conecte-se à instância do SQL.  
  
2. Verifique se não há nenhuma conexão aberta ao banco de dados. Se você estiver usando o SQL Server, você poderá [definir o banco de dados para o modo de usuário único](../../relational-databases/databases/set-a-database-to-single-user-mode.md) para fechar todas as conexões abertas e impedir que outros usuários se conectem enquanto você estiver alterando o nome do banco de dados.  
  
3. No Pesquisador de Objetos, expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados a renomear e, em seguida, clique em **Renomear**.  
  
4. Digite o novo nome do banco de dados e, depois, clique em **OK**.  
  
5. Opcionalmente, se o banco de dados for o banco de dados padrão, confira [Redefinir o banco de dados padrão após a renomeação](#reset-your-default-database-after-rename).

## <a name="rename-a-database-using-transact-sql"></a>Renomear um banco de dados usando o Transact-SQL  
  
### <a name="to-rename-a-sql-server-database-by-placing-it-in-single-user-mode"></a>Para renomear um banco de dados do SQL Server colocando-o no modo de usuário único

Use as etapas a seguir para renomear um banco de dados do SQL Server usando o T-SQL no SQL Server Management Studio, incluindo as etapas para colocar o banco de dados no modo de usuário único. Depois de renomeá-lo, coloque o banco de dados novamente em modo multiusuário.
  
1. Conecte-se ao banco de dados `master` para sua instância.  
2. Abra uma janela de consulta.  
3. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo altera o nome do banco de dados `MyTestDatabase` para `MyTestDatabaseCopy`.
  
   ```sql
   USE master;  
   GO  
   ALTER DATABASE MyTestDatabase SET SINGLE_USER WITH ROLLBACK IMMEDIATE
   GO
   ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
   GO  
   ALTER DATABASE MyTestDatabaseCopy SET MULTI_USER
   GO
   ```  

4. Opcionalmente, se o banco de dados for o banco de dados padrão, confira [Redefinir o banco de dados padrão após a renomeação](#reset-your-default-database-after-rename).

### <a name="to-rename-an-azure-sql-database-database"></a>Para renomear um banco de dados do Banco de Dados SQL do Azure

Use as etapas a seguir para renomear um Banco de Dados SQL do Azure usando o T-SQL no SQL Server Management Studio.
  
1. Conecte-se ao banco de dados `master` para sua instância.  
2. Abra uma janela de consulta.
3. Garanta que ninguém esteja usando o banco de dados.
4. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo altera o nome do banco de dados `MyTestDatabase` para `MyTestDatabaseCopy`.
  
   ```sql
   ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
   ```  

## <a name="backup-after-renaming-a-database"></a>Fazer backup depois de renomear um banco de dados  

Depois de renomear um banco de dados no SQL Server, faça backup do banco de dados `master`. No Banco de Dados SQL do Azure isso não é necessário, pois os backups ocorrem automaticamente.  
  
## <a name="reset-your-default-database-after-rename"></a>Redefinir o banco de dados padrão após a renomeação

Se o banco de dados que você está renomeando tiver sido definido como o banco de dados padrão, use o seguinte comando para redefinir o padrão para o banco de dados renomeado:


```sql
USE [master]
GO
ALTER LOGIN [your-login] WITH DEFAULT_DATABASE=[new-database-name]
GO
```


## <a name="see-also"></a>Consulte Também

- [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)
- [Identificadores de banco de dados](../../relational-databases/databases/database-identifiers.md)  
