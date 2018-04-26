---
title: FileStream e FileTable armazenados do sistema procedimentos (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 19ee3e87d2878dcf56d0d8d26e79d1116f657fa6
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>(Transact-SQL) de procedimentos armazenados do sistema de FILESTREAM e FileTable
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Esta seção descreve os procedimentos armazenados do sistema para o recurso de FileTable e Filestream.  

## <a name="filestream-and-filetable-system-stored-procedures"></a>Procedimentos armazenados do sistema de FILESTREAM e Filetable
  [sp_filestream_force_garbage_collection (Transact-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   Força a execução do coletor de lixo FILESTREAM, excluindo qualquer arquivo FILESTREAM desnecessário.

  [sp_kill_filestream_non_transacted_handles (Transact-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  Fecha identificadores de arquivos não transacionais para dados de FileTable.


## <a name="see-also"></a>Consulte também
[FileStream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[FileStream e exibições de gerenciamento dinâmico de FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[FileStream e exibições do catálogo FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
