---
title: sys.remote_data_archive_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.remote_data_archive_databases
- sys.remote_data_archive_databases_TSQL
- remote_data_archive_databases
- remote_data_archive_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.remote_data_archive_databases catalog view
ms.assetid: 25bffb0c-9821-40b4-88cf-75f854891a09
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
manager: craigg
ms.openlocfilehash: 74a44e8c3e6b0be026ac716d43b539869345b3b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "64945608"
---
# <a name="stretch-database-catalog-views---sysremotedataarchivedatabases"></a>Stretch Database exibições do catálogo – sys. remote_data_archive_databases
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada banco de dados remoto que armazena dados de um banco de dados de local habilitada para Stretch.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|O identificador de local gerado automaticamente do banco de dados remoto.|  
|**remote_database_name**|**sysname**|O nome do banco de dados remoto.|  
|**data_source_id**|**int**|A fonte de dados usada para se conectar ao servidor remoto|  
  
## <a name="see-also"></a>Consulte também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
