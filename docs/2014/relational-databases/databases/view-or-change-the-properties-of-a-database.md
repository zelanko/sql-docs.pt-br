---
title: Exibir ou alterar as propriedades de um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- displaying databases
- database viewing [SQL Server]
- databases [SQL Server], viewing
- viewing databases
ms.assetid: 9e8ac097-84b7-46c7-85e3-c1e79f94d747
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 10ad92286011f6f81fbaff5ab4908007e16bdd45
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62870946"
---
# <a name="view-or-change-the-properties-of-a-database"></a>Exibir ou alterar as propriedades de um banco de dados
  Este tópico descreve como exibir ou alterar os propriedades de um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Depois de alterar uma propriedade de banco de dados, a modificação entra em vigor imediatamente.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para exibir ou alterar as propriedades de um banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Quando AUTO_CLOSE for ON, algumas colunas da exibição de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) e da função DATABASEPROPERTYEX retornarão NULL, pois o banco de dados não está disponível para recuperar os dados. Para resolver isso, execute uma instrução USE para abrir o banco de dados.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-properties-of-a-database"></a>Para exibir ou alterar as propriedades de um banco de dados  
  
1.  No Pesquisador de **objetos**, conecte-se a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]uma instância do e expanda essa instância.  
  
2.  Expanda **Banco de Dados**, clique com o botão direito do mouse no banco de dados para exibi-lo e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Banco de Dados** , selecione uma página para exibir as informações correspondentes. Por exemplo, selecione a página **Arquivos** para exibir os dados e as informações do arquivo de log.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-a-property-of-a-database-by-using-databasepropertyex"></a>Para exibir uma propriedade de um banco de dados usando DATABASEPROPERTYEX  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa a função do sistema [DATABASEPROPERTYEX](/sql/t-sql/functions/databasepropertyex-transact-sql) para retornar o status da opção de banco de dados AUTO_SHRINK no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Um valor de retorno 1 significa que a opção está definida como ON e um valor de retorno 0 significa que a opção está definida como OFF.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT DATABASEPROPERTYEX('AdventureWorks2012', 'IsAutoShrink');  
GO  
  
```  
  
#### <a name="to-view-the-properties-of-a-database-by-querying-sysdatabases"></a>Para exibir as propriedades de um banco de dados consultando sys.databases  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo consulta a exibição de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) para exibir várias propriedades do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Este exemplo retorna o número de identificação de banco de dados (`database_id`), se o banco de dados for somente leitura ou de leitura/gravação (`is_read_only`), a ordenação do banco de dados (`collation_name`) e o nível de compatibilidade do banco de dados (`compatibility_level`).  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT database_id, is_read_only, collation_name, compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
  
```  
  
#### <a name="to-change-the-properties-of-a-database"></a>Para alterar as propriedades de um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta. O exemplo determina o estado de isolamento de instantâneo no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , altera o estado da propriedade e verifique a alteração.  
  
     Para determinar o estado de isolamento de instantâneo, selecione a primeira instrução `SELECT` e clique em **Executar**.  
  
     Para alterar o estado de isolamento de instantâneo, selecione a primeira instrução `ALTER DATABASE` e clique em **Executar**.  
  
     Para verificar a alteração, selecione a segunda instrução `SELECT` e clique em **Executar**.  
  
 [!code-sql[DatabaseDDL#AlterDatabase9](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase9)]  
  
## <a name="see-also"></a>Consulte Também  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [ALTER DATABASE SET HADR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-hadr)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)   
 [Espelhamento de banco de dados ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)   
 [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
  
