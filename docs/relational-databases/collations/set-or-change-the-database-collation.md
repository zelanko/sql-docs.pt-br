---
title: Definir ou alterar o agrupamento de banco de dados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: collations
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Active
ms.openlocfilehash: e39ed48b206151e6953ab2f49aa469a356162f87
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/12/2018
---
# <a name="set-or-change-the-database-collation"></a>Definir ou alterar o agrupamento de banco de dados
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Este tópico descreve como definir e alterar o agrupamento de banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se nenhum agrupamento for especificado, será usado o agrupamento do servidor.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para definir ou alterar o agrupamento de banco de dados**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Os agrupamentos somente Unicode do Windows podem ser usados somente com a cláusula COLLATE para aplicar agrupamentos aos tipos de dados **nchar**, **nvarchar**e **ntext** em dados nos níveis de coluna e de expressão. Não é possível usá-los com a cláusula COLLATE para alterar o agrupamento de uma instância de banco de dados ou de servidor.  
  
-   Se o agrupamento especificado ou o agrupamento usado pelo objeto referenciado usar uma página de código sem suporte no Windows, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] exibirá um erro.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Você pode encontrar os nomes de agrupamento com suporte no [Nome de agrupamento do Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) e [Nome de agrupamento do SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)ou pode usar a função do sistema [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) .  
  
-   Ao alterar o agrupamento de banco de dados, você altera o seguinte:  
  
    -   Qualquer coluna **char**, **varchar**, **text**, **nchar**, **nvarchar**ou **ntext** nas tabelas do sistema são alteradas para o novo agrupamento.  
  
    -   Todos os parâmetros **char**, **varchar**, **text**, **nchar**, **nvarchar**ou **ntext** e valores de retorno escalar para procedimentos armazenados e funções definidas pelo usuário existentes são alterados para o novo agrupamento.  
  
    -   Os tipos de dados do sistema **char**, **varchar**, **text**, **nchar**, **nvarchar**ou **ntext** e todos os tipos de dados definidos pelo usuário com base nesses tipos de dados do sistema são alterados para o novo agrupamento padrão.  
  
-   Você pode alterar o agrupamento de qualquer novo objeto que seja criado em um banco de dados de usuário, usando a cláusula COLLATE da instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) . Essa instrução não altera o agrupamento das colunas em nenhuma tabela existente definida pelo usuário. Essas podem ser alteradas usando-se a cláusula COLLATE de [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 CREATE DATABASE  
 Requer a permissão CREATE DATABASE no banco de dados **mestre** ou requer a permissão CREATE ANY DATABASE ou ALTER ANY DATABASE.  
  
 ALTER DATABASE  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>Para definir ou alterar o agrupamento de banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], expanda essa instância e expanda **Bancos de Dados**.  
  
2.  Se você estiver criando um novo banco de dados, clique com o botão direito do mouse em **Bancos de Dados** e clique em **Novo Banco de Dados**. Se você não desejar o agrupamento padrão, clique na página **Opções** e selecione um agrupamento na lista suspensa **Agrupamento** .  
  
     De maneira alternativa, se o banco de dados já existir, clique com o botão direito do mouse no banco de dados desejado e clique em **Propriedades**. Clique na página **Opções** e selecione um agrupamento na lista suspensa **Agrupamento** .  
  
3.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-set-the-database-collation"></a>Para definir o agrupamento de banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar a cláusula [COLLATE](~/t-sql/statements/collations.md) para especificar um nome de agrupamento. O exemplo cria o banco de dados `MyOptionsTest` que usa o agrupamento `Latin1_General_100_CS_AS_SC` . Depois de criar o banco de dados, execute a instrução `SELECT` para verificar a configuração.  
  
```sql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE Latin1_General_100_CS_AS_SC;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
#### <a name="to-change-the-database-collation"></a>Para alterar o agrupamento de banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar a cláusula [COLLATE](~/t-sql/statements/collations.md) em uma instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) para alterar o nome do agrupamento. Execute a instrução `SELECT` para verificar a alteração.  
  
```sql  
USE master;  
GO  
ALTER DATABASE MyOptionsTest  
COLLATE French_CI_AS ;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte a agrupamentos e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Nome de agrupamento do SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)   
 [Nome de agrupamento do Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)   
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [Precedência de agrupamento &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
