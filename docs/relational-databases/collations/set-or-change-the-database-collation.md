---
description: Definir ou alterar a ordenação de banco de dados
title: Definir ou alterar a ordenação de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7fbaf22758dcf62d2159e63ee3af3c0507f3f607
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460569"
---
# <a name="set-or-change-the-database-collation"></a>Definir ou alterar a ordenação de banco de dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como definir e alterar a ordenação de banco de dados usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se nenhuma ordenação for especificada, será usada a ordenação do servidor.  
  
> [!IMPORTANT]
> A declaração `ALTER DATABASE COLLATE` no Banco de Dados SQL do Azure não tem suporte.

 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para definir ou alterar a ordenação de banco de dados**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   As ordenações somente Unicode do Windows podem ser usadas somente com a cláusula COLLATE para aplicar ordenações aos tipos de dados **nchar**, **nvarchar** e **ntext** em dados nos níveis de coluna e de expressão. Não é possível usá-los com a cláusula COLLATE para alterar a ordenação de uma instância de banco de dados ou de servidor.  
  
-   Se a ordenação especificada ou a ordenação usada pelo objeto referenciado usar uma página de código sem suporte no Windows, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] exibirá um erro.  

###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
Você pode encontrar os nomes de ordenação com suporte no [Windows Collation Name &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) e [SQL Server Collation Name &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md) ou pode usar a função do sistema [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) .  
  
Ao alterar a ordenação de banco de dados, você altera o seguinte:  
  
-   Qualquer coluna **char**, **varchar**, **text**, **nchar**, **nvarchar** ou **ntext** nas tabelas do sistema são alteradas para a nova ordenação.  
  
-   Todos os parâmetros **char**, **varchar**, **text**, **nchar**, **nvarchar** ou **ntext** e valores de retorno escalar para procedimentos armazenados e funções definidas pelo usuário existentes são alterados para a nova ordenação.  
  
-   Os tipos de dados do sistema **char**, **varchar**, **text**, **nchar**, **nvarchar** ou **ntext** e todos os tipos de dados definidos pelo usuário com base nesses tipos de dados do sistema são alterados para a nova ordenação padrão.  
  
Você pode alterar a ordenação de qualquer novo objeto que seja criado em um banco de dados de usuário usando a cláusula `COLLATE` da instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md). Essa instrução **não altera** a ordenação das colunas em nenhuma tabela existente definida pelo usuário. Isso pode ser alterado usando a cláusula `COLLATE` de [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  

> [!IMPORTANT]
> Alterar a ordenação de um banco de dados ou de colunas individuais **não modifica** os dados subjacentes já armazenados em tabelas existentes. A menos que o seu aplicativo manipule explicitamente a conversão de dados e a comparação entre diferentes ordenações, é recomendável que você migre os dados existentes no banco de dados para a nova ordenação. Isso elimina o risco de que os aplicativos modifiquem incorretamente os dados, o que decorreria em possíveis resultados incorretos ou na perda de dados silenciosa.   

Quando uma ordenação de banco de dados for alterada, somente as novas tabelas herdarão a nova ordenação de banco de dados por padrão. Há várias alternativas para converter dados existentes para a nova ordenação:
-  Converter os dados in-loco. Para converter a ordenação de uma coluna em uma tabela existente, confira [Definir ou alterar a ordenação de colunas](../../relational-databases/collations/set-or-change-the-column-collation.md). Essa operação é fácil de implementar, mas pode se tornar um problema de bloqueio para grandes tabelas e aplicativos ocupados. Confira o seguinte exemplo de uma conversão in-loco da coluna `MyString` para uma nova ordenação:

   ```sql
   ALTER TABLE dbo.MyTable
   ALTER COLUMN MyString VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8;
   ```

-  Copiar dados para novas tabelas que usam a nova ordenação e substitua as tabelas originais no mesmo banco de dados. Crie uma tabela no banco de dados atual que herdará a ordenação de banco de dados, copie os dados entre a tabela antiga e a nova tabela, remova a tabela original e renomeie a nova tabela com o nome da tabela original. Essa é uma operação mais rápida do que uma conversão in-loco, mas pode se tornar um desafio lidar com esquemas complexos com dependências como restrições de Chave Estrangeira, restrições de Chave Primária e Gatilhos. Ela também exigiria uma sincronização de dados final entre a nova tabela e a original antes do limiar final se os dados continuassem sendo alterados pelos aplicativos. Confira o seguinte exemplo de uma conversão "copiar e substituir" da coluna `MyString` em uma nova ordenação:

   ```sql
   CREATE TABLE dbo.MyTable2 (MyString VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8); 
   
   INSERT INTO dbo.MyTable2 
   SELECT * FROM dbo.MyTable; 
   
   DROP TABLE dbo.MyTable; 
   
   EXEC sp_rename 'dbo.MyTable2', 'dbo.MyTable’;
   ```

-  Copiar dados para um novo banco de dados que usa a nova ordenação e substitua o banco de dados original. Crie um banco de dados usando a nova ordenação e transfira os dados do banco de dados original com ferramentas como o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou o Assistente de Importação/Exportação no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Essa é uma abordagem mais simples para esquemas complexos. Ela também exigiria uma sincronização de dados final entre o novo banco de dados e o original antes do limiar final se os dados continuassem sendo alterados pelos aplicativos.
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 A criação de um novo banco de dados requer a permissão `CREATE DATABASE` no banco de dados **mestre** ou as permissões `CREATE ANY DATABASE` ou `ALTER ANY DATABASE`.  
  
 A alteração da ordenação de um banco de dados existente requer a permissão `ALTER` no banco de dados.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>Para definir ou alterar a ordenação de banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], expanda essa instância e expanda **Bancos de Dados**.  
  
2.  Se você estiver criando um novo banco de dados, clique com o botão direito do mouse em **Bancos de Dados** e clique em **Novo Banco de Dados**. Se você não desejar a ordenação padrão, clique na página **Opções** e selecione uma ordenação na lista suspensa **Ordenação**.  
  
     De maneira alternativa, se o banco de dados já existir, clique com o botão direito do mouse no banco de dados desejado e clique em **Propriedades**. Clique na página **Opções** e selecione uma ordenação na lista suspensa **Ordenação**.  
  
3.  Quando terminar, clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-set-the-database-collation"></a>Para definir a ordenação de banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar a cláusula [COLLATE](~/t-sql/statements/collations.md) para especificar um nome de ordenação. O exemplo cria o banco de dados `MyOptionsTest` que usa a ordenação `Latin1_General_100_CS_AS_SC`. Depois de criar o banco de dados, execute a instrução `SELECT` para verificar a configuração.  
  
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
  
#### <a name="to-change-the-database-collation"></a>Para alterar a ordenação de banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar a cláusula [COLLATE](~/t-sql/statements/collations.md) em uma instrução [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) para alterar o nome da ordenação. Execute a instrução `SELECT` para verificar a alteração.  
  
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
 [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Nome de ordenação do SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)   
 [Nome de ordenação do Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)   
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [Precedência de ordenação &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
