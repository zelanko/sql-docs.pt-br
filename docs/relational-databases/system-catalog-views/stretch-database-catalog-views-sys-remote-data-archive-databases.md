---
title: sys. remote_data_archive_databases (Transact-SQL) | Microsoft Docs
description: Saiba como o sys. remote_data_archive_databases contém uma linha para cada banco de dados remoto que armazena o dado de um banco de dados local habilitado para Stretch.
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
ms.openlocfilehash: e192a70c1d8f46b7ad89844a3b38019ab6364cc1
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248145"
---
# <a name="stretch-database-catalog-views---sysremote_data_archive_databases"></a>Stretch Database exibições do catálogo-sys. remote_data_archive_databases
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Contém uma linha para cada banco de dados remoto que armazena os dados de um banco de dado local habilitado para Stretch.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**remote_database_id**|**int**|O identificador local gerado automaticamente do banco de dados remoto.|  
|**remote_database_name**|**sysname**|O nome do banco de dados remoto.|  
|**data_source_id**|**int**|A fonte de dados usada para se conectar ao servidor remoto|  
  
## <a name="see-also"></a>Consulte Também  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
