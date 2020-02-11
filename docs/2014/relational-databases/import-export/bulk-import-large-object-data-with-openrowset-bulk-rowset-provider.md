---
title: Importação em massa de dados de objeto grande usando o provedor de conjunto de linhas OPENROWSET em massa (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f6fe945ea90a150397abecfd83f0ce1c945f217c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66012109"
---
# <a name="bulk-import-large-object-data-by-using-the-openrowset-bulk-rowset-provider-sql-server"></a>Importando em massa dados de objeto grande usando o provedor de conjunto de linhas em massa OPENROWSET (SQL Server)
  O Provedor de Conjunto de Linhas em Massa OPENROWSET do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a importação em massa de um arquivo de dados como dados de objeto grande.  
  
 Os tipos de dados de objeto grande com suporte no Provedor de Conjuntos de Linhas em Massa OPENROWSET são **varbinary**(max) ou **image**, **varchar**(max) ou **text**e **nvarchar**(max) ou **ntext**.  
  
> [!NOTE]  
>  Os tipos de dados **image**, **text** e **ntext** foram preteridos.  
  
 A cláusula OPENROWSET BULK oferece suporte a três opções que importam o conteúdo de um arquivo de dados como um conjunto de linhas com linha e coluna únicas. Você pode especificar uma dessas opções de objeto grande, em vez de usar um arquivo de formato. Essas opções são as seguintes:  
  
 SINGLE_BLOB  
 Lê o conteúdo de *data_file* como uma linha única, retorna o conteúdo como um conjunto de linhas de coluna única do tipo **varbinary(max)** .  
  
 SINGLE_CLOB  
 Lê os conteúdos do arquivo de dados especificado como caracteres, retorna os conteúdos como um conjunto de linhas de linha única e coluna única do tipo **varchar(max)** , usando a ordenação do banco de dados atual, como um text ou documento do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word.  
  
 SINGLE_NCLOB  
 Lê os conteúdos do arquivo de dados especificados como Unicode, retorna os conteúdos como um conjunto de linhas de linha única e coluna única do tipo **nvarchar(max)** , usando a ordenação do banco de dados atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Importar dados em massa usando BULK INSERT ou OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Manter valores nulos ou use os valores padrão durante a importação em massa &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)  
  
  
