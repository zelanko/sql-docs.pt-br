---
title: Exibir informações de agrupamento | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 034a9e1dc97492810f8d20b253b544344862dfe5
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39558139"
---
# <a name="view-collation-information"></a>Exiba informações de agrupamento
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
##  <a name="Top"></a> Você pode exibir o agrupamento de um servidor, banco de dados ou coluna no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando as opções de menu do Pesquisador de Objetos ou usando o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
##  <a name="Procedures"></a> Como exibir uma configuração de agrupamento  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para exibir uma configuração de agrupamento para um servidor (instância do SQL Server) no Pesquisador de Objetos**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Clique com o botão direito do mouse na instância e selecione **Propriedades**.  
  
 **Para exibir uma configuração de agrupamento para um banco de dados no Pesquisador de Objetos**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Banco de Dados**, clique com o botão direito do mouse no banco de dados e selecione **Propriedades**.  
  
 **Para exibir uma configuração de agrupamento para uma coluna no Pesquisador de Objetos**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados e, por fim, expanda **Tabelas**.  
  
3.  Expanda a tabela que contém a coluna e expanda **Colunas**.  
  
4.  Clique com o botão direito do mouse na coluna e selecione **Propriedades**. Se a propriedade de agrupamento estiver vazia, a coluna não será um tipo de dados de caractere.  
  
###  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para exibir a configuração de agrupamento de um servidor**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a função de sistema SERVERPROPERTY.  
  
    ```  
    SELECT CONVERT (varchar, SERVERPROPERTY('collation'));  
    ```  
  
3.  Se desejar, você pode usar o procedimento armazenado de sistema sp_helpsort.  
  
    ```  
    EXECUTE sp_helpsort;  
    ```  
  
 **Para exibir todos os agrupamentos com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a função de sistema SERVERPROPERTY.  
  
    ```  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **Para exibir a configuração de agrupamento de um banco de dados.**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a exibição de catálogo de sistema do sys.databases.  
  
    ```  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  Se desejar, você pode usar a função de sistema DATABASEPROPERTYEX.  
  
    ```  
    SELECT CONVERT (varchar, DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **Para exibir a configuração de agrupamento de uma coluna**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a exibição de catálogo de sistema sys.columns.  
  
    ```  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Precedência de agrupamento &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [sp_helpsort &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsort-transact-sql.md)  
  
  
