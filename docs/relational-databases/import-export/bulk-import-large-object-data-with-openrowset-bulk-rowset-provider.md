---
title: Importando em massa dados de objeto grande com o provedor de conjunto de linhas em massa OPENROWSET | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SINGLE_NCLOB option
- bulk rowset providers [SQL Server]
- bulk importing [SQL Server], data formats
- OPENROWSET function, bulk importing large data
- SINGLE_CLOB option
- data formats [SQL Server], large-object data
- large data, bulk imports
- SINGLE_BLOB option
ms.assetid: 171cdd5c-1e47-4bd7-b99a-4f0fd4e10526
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f2e2d3cb37032842ca391d4762a990b2808f2c0e
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="bulk-import-large-object-data-with-openrowset-bulk-rowset-provider"></a>Importando em massa dados de objeto grande com o provedor de conjunto de linhas em massa OPENROWSET
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  O Provedor de Conjunto de Linhas em Massa OPENROWSET do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a importação em massa de um arquivo de dados como dados de objeto grande.  
  
 Os tipos de dados de objeto grande com suporte no Provedor de Conjuntos de Linhas em Massa OPENROWSET são **varbinary**(max) ou **image**, **varchar**(max) ou **text**e **nvarchar**(max) ou **ntext**.  
  
> [!NOTE]  
>  Os tipos de dados **image**, **text** e **ntext** foram preteridos.  
  
 A cláusula OPENROWSET BULK oferece suporte a três opções que importam o conteúdo de um arquivo de dados como um conjunto de linhas com linha e coluna únicas. Você pode especificar uma dessas opções de objeto grande, em vez de usar um arquivo de formato. Essas opções são as seguintes:  
  
 SINGLE_BLOB  
 Lê o conteúdo de *data_file* como uma linha única, retorna o conteúdo como um conjunto de linhas de coluna única do tipo **varbinary(max)**.  
  
 SINGLE_CLOB  
 Lê os conteúdos do arquivo de dados especificado como caracteres, retorna os conteúdos como um conjunto de linhas de linha única e coluna única do tipo **varchar(max)**, usando o agrupamento do banco de dados atual, como um text ou documento do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word.  
  
 SINGLE_NCLOB  
 Lê os conteúdos do arquivo de dados especificados como Unicode, retorna os conteúdos como um conjunto de linhas de linha única e coluna única do tipo **nvarchar(max)**, usando o agrupamento do banco de dados atual.  
  
## <a name="see-also"></a>Consulte também  
 [Importar dados em massa usando BULK INSERT ou OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)  
  
  
