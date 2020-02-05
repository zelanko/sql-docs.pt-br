---
title: Exibir informações de ordenação | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], view
ms.assetid: 1338b4ea-7142-44bc-a3b9-44e54431405f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bedae7661398ed4281f2da460ad7ce16b5dd82de
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68841617"
---
# <a name="view-collation-information"></a>Exibir informações de ordenação
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
    
<a name="Top"></a> Você pode exibir a ordenação de um servidor, banco de dados ou coluna no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usando as opções de menu do Pesquisador de Objetos ou usando o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
##  <a name="Procedures"></a> Como exibir uma configuração de ordenação  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
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
  
###  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para exibir a configuração de ordenação de um servidor**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a função de sistema SERVERPROPERTY.  
  
    ```sql  
    SELECT CONVERT (varchar(256), SERVERPROPERTY('collation'));  
    ```  
  
3.  Se desejar, você pode usar o procedimento armazenado de sistema sp_helpsort.  
  
    ```sql  
    EXECUTE sp_helpsort;  
    ```  
  
 **Para exibir todas as ordenações com suporte no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a função de sistema SERVERPROPERTY.  
  
    ```sql  
    SELECT name, description FROM sys.fn_helpcollations();  
    ```  
  
 **Para exibir a configuração de ordenação de um banco de dados.**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a exibição de catálogo de sistema do sys.databases.  
  
    ```sql  
    SELECT name, collation_name FROM sys.databases;  
    ```  
  
3.  Se desejar, você pode usar a função de sistema DATABASEPROPERTYEX.  
  
    ```sql  
    SELECT CONVERT (varchar(256), DATABASEPROPERTYEX('database_name','collation'));  
    ```  
  
 **Para exibir a configuração de ordenação de uma coluna**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a exibição de catálogo de sistema sys.columns.  
  
    ```sql  
    SELECT name, collation_name FROM sys.columns WHERE name = N'<insert character data type column name>';  
    ```  
  
 **Para exibir as configurações de agrupamentos para tabelas e colunas**  

1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e, na barra de ferramentas, clique em **Nova Consulta**.  
  
2.  Na janela de consulta, insira a instrução a seguir que usa a exibição de catálogo de sistema sys.columns.  
  
    ```sql  
    SELECT t.name TableName, c.name ColumnName, collation_name  
    FROM sys.columns c  
    inner join sys.tables t on c.object_id = t.object_id;  
    ```  



## <a name="see-also"></a>Consulte Também  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Precedência de ordenação &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [Suporte a ordenações e a Unicode](../../relational-databases/collations/collation-and-unicode-support.md)      
 [sp_helpsort &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsort-transact-sql.md)  
  
  
