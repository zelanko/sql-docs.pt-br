---
description: Exibições de gerenciamento dinâmico de fluxo de arquivos e FileTable (Transact-SQL)
title: Exibições de gerenciamento dinâmico de FileStream e Filetable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], dynamic management views
ms.assetid: e50a135d-6644-42a4-a0df-1c7a2b722051
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 268499cff0d6d967134cd8d28a6842df04fba0cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544835"
---
# <a name="filestream-and-filetable-dynamic-management-views-transact-sql"></a>Exibições de gerenciamento dinâmico de fluxo de arquivos e FileTable (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Esta seção descreve as exibições de gerenciamento dinâmico relacionadas aos recursos FILESTREAM e FileTable.  
  
## <a name="filestream-dynamic-management-views-and-functions"></a>Exibições e funções de gerenciamento dinâmico de fluxo de arquivos  
 [sys.dm_filestream_file_io_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-handles-transact-sql.md)  
 Exibe os identificadores de arquivos transacionais atualmente abertos.  
  
 [sys.dm_filestream_file_io_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-file-io-requests-transact-sql.md)  
 Exibe as solicitações atuais de entrada e saída de arquivo.  
  
## <a name="filetable-dynamic-management-views-and-functions"></a>Exibições e funções de gerenciamento dinâmico de FileTable  
 [sys.dm_filestream_non_transacted_handles &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md)  
 Exibe os identificadores de arquivo não transacionais atualmente abertos para dados de FileTable.  

## <a name="see-also"></a>Consulte Também
[Fluxo de arquivos](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[Exibições de catálogo de fluxo de arquivos e FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[Procedimentos armazenados de fluxo de arquivos e FileTable (Transact-SQL)](../system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)
  
