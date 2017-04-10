---
title: "Exibir dados e informa&#231;&#245;es de espa&#231;o de log para um banco de dados | Microsoft Docs"
ms.custom: ""
ms.date: "08/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "logs [SQL Server], espaço"
  - "informações de status [SQL Server], espaço"
  - "exibindo informações de espaço"
  - "espaço em disco [SQL Server], exibindo"
  - "bancos de dados [SQL Server], espaço usado"
  - "exibindo informações de espaço"
  - "alocação de espaço [SQL Server], exibindo"
  - "espaço de dados [SQL Server]"
ms.assetid: c7b99463-4bab-4e9b-9217-fcb0898dc757
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Exibir dados e informa&#231;&#245;es de espa&#231;o de log para um banco de dados
  Este tópico descreve como exibir os dados e as informações de espaço de log para um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  

  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 A permissão para executar **sp_spaceused** é concedida à função **public**. Somente os membros da função de banco de dados fixa **db_owner** podem especificar o parâmetro **@updateusage**.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para exibir dados e informações de espaço de log para um banco de dados  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e expanda essa instância.  
  
2.  Expanda os **Bancos de dados**.  
  
3.  Clique com o botão direito do mouse em um banco de dados, aponte para **Relatórios**, aponte para **Relatórios Padrão** e clique em **Uso do Disco**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para exibir dados e informações de espaço de log para um banco de dados usando sp_spaceused  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa o procedimento armazenado de sistema [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) para relatar informações de espaço em disco para a tabela `Vendor` e seus índices.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
#### Para exibir dados e informações de espaço de log para um banco de dados consultando sys.database_files  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo consulta a exibição de catálogo [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) para retornar informações específicas sobre os dados e arquivos de log no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```tsql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name, type_desc, physical_name, size, max_size  
FROM sys.database_files ;  
GO  
  
```  
  
## Consulte também  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [Adicionar arquivos de dados ou de log a um banco de dados](../../relational-databases/databases/add-data-or-log-files-to-a-database.md)   
 [Excluir arquivos de dados ou de log de um banco de dados](../../relational-databases/databases/delete-data-or-log-files-from-a-database.md)  
  
  