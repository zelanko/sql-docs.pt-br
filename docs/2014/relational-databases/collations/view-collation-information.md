---
title: Exibir informações de ordenação | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 995e559cfd7ca871f5abd90751f2f79167bdf76f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970541"
---
# <a name="view-collation-information"></a>Exibir informações de ordenação
    
##  <a name="you-can-view-the-collation-of-a-server-database-or-column-in-ssmanstudiofull-using-object-explorer-menu-options-or-by-using-tsql"></a><a name="Top"></a> Você pode exibir a ordenação de um servidor, banco de dados ou coluna no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando as opções de menu do Pesquisador de Objetos ou usando o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
##  <a name="how-to-view-a-collation-setting"></a><a name="Procedures"></a> Como exibir uma configuração de ordenação  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para exibir uma configuração de ordenação para um servidor (instância do SQL Server) no Pesquisador de Objetos**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Clique com o botão direito do mouse na instância e selecione **Propriedades**.  
  
 **Para exibir uma configuração de ordenação para um banco de dados no Pesquisador de Objetos**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Banco de Dados**, clique com o botão direito do mouse no banco de dados e selecione **Propriedades**.  
  
 **Para exibir uma configuração de ordenação para uma coluna no Pesquisador de Objetos**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados e, por fim, expanda **Tabelas**.  
  
3.  Expanda a tabela que contém a coluna e expanda **Colunas**.  
  
4.  Clique com o botão direito do mouse na coluna e selecione **Propriedades**. Se a propriedade de ordenação estiver vazia, a coluna não será um tipo de dados de caractere.  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para exibir a configuração de ordenação de um servidor**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a função de sistema SERVERPROPERTY.  
  
    ```  
    SELECT CONVERT (varchar, SERVERPROPERTY('collation'));  
    ```  
  
3.  Se desejar, você pode usar o procedimento armazenado de sistema sp_helpsort.  
  
    ```  
    EXECUTE sp_helpsort;  
    ```  
  
 **Para exibir todas as ordenações com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a função de sistema SERVERPROPERTY.  
  
    ```  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **Para exibir a configuração de ordenação de um banco de dados.**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a exibição de catálogo de sistema do sys.databases.  
  
    ```  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  Se desejar, você pode usar a função de sistema DATABASEPROPERTYEX.  
  
    ```  
    SELECT CONVERT (varchar, DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **Para exibir a configuração de ordenação de uma coluna**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a exibição de catálogo de sistema sys.columns.  
  
    ```  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;SERVERPROPERTY &#40;Transact-SQL](/sql/t-sql/functions/serverproperty-transact-sql)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [&#41;sys. Columns &#40;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-columns-transact-sql)   
 [Precedência de ordenação &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [sp_helpsort &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsort-transact-sql)  
  
  
