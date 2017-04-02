---
title: "Importando em massa dados de objeto grande usando o provedor de conjunto de linhas em massa OPENROWSET (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-bulk-import-export"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "opção SINGLE_NCLOB"
  - "provedores de conjuntos de linhas em massa [SQL Server]"
  - "importação em massa [SQL Server], formatos de dados"
  - "Função OPENROWSET, dados grandes de importação em massa"
  - "opção SINGLE_CLOB"
  - "formatos de dados [SQL Server], dados de objeto grande"
  - "dados grandes, importações em massa"
  - "opção SINGLE_BLOB"
ms.assetid: 171cdd5c-1e47-4bd7-b99a-4f0fd4e10526
caps.latest.revision: 16
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
---
# Importando em massa dados de objeto grande usando o provedor de conjunto de linhas em massa OPENROWSET (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  O Provedor de Conjunto de Linhas em Massa OPENROWSET do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a importação em massa de um arquivo de dados como dados de objeto grande.  
  
 Os tipos de dados de objeto grande com suporte no Provedor de Conjuntos de Linhas em Massa OPENROWSET são **varbinary**(max) ou **image**, **varchar**(max) ou **text** e **nvarchar**(max) ou **ntext**.  
  
> [!NOTE]  
>  Os tipos de dados **image**, **text** e **ntext** foram preteridos.  
  
 A cláusula OPENROWSET BULK oferece suporte a três opções que importam o conteúdo de um arquivo de dados como um conjunto de linhas com linha e coluna únicas. Você pode especificar uma dessas opções de objeto grande, em vez de usar um arquivo de formato. Essas opções são as seguintes:  
  
 SINGLE_BLOB  
 Lê o conteúdo de *data_file* como uma linha única, retorna o conteúdo como um conjunto de linhas de coluna única do tipo **varbinary(max)**.  
  
 SINGLE_CLOB  
 Lê os conteúdos do arquivo de dados especificado como caracteres, retorna os conteúdos como um conjunto de linhas de linha única e coluna única do tipo **varchar(max)**, usando o agrupamento do banco de dados atual, como um text ou documento do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word.  
  
 SINGLE_NCLOB  
 Lê os conteúdos do arquivo de dados especificados como Unicode, retorna os conteúdos como um conjunto de linhas de linha única e coluna única do tipo **nvarchar(max)**, usando o agrupamento do banco de dados atual.  
  
## Consulte também  
 [Importar dados em massa usando BULK INSERT ou OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  