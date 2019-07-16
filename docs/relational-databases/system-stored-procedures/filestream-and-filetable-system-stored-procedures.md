---
title: FileStream e FileTable procedimentos armazenados (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1ebcaf4659d7be880f0f0e901b2eadcc9002b2d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942248"
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>(Transact-SQL) de procedimentos armazenados do sistema de FILESTREAM e FileTable
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Esta seção descreve os procedimentos armazenados do sistema para o recurso de FileTable e Filestream.  

## <a name="filestream-and-filetable-system-stored-procedures"></a>Procedimentos armazenados do sistema de FILESTREAM e Filetable
  [sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   Força a execução do coletor de lixo FILESTREAM, excluindo qualquer arquivo FILESTREAM desnecessário.

  [sp_kill_filestream_non_transacted_handles (Transact-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  Fecha identificadores de arquivos não transacionais para dados de FileTable.


## <a name="see-also"></a>Confira também
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[Exibições de gerenciamento dinâmico de fluxo de arquivos e FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Exibições de catálogo de fluxo de arquivos e FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
