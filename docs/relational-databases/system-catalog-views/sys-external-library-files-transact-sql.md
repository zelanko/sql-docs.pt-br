---
title: sys.external_library_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_library_files catalog view
author: jeannt
ms.author: jeannt
manager: craigg
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 67b5988b1000d54ab929da85e03a63b11dfee5ee
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39533246"
---
# <a name="sysexternallibraryfiles-transact-sql"></a>sys.external_library_files (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Lista uma linha para cada arquivo que compõe uma biblioteca externa.

|Nome da coluna |Tipo de dados |Description|
|------|------|-----|
|external_library_id | INT |ID do objeto de biblioteca externa. |
|content |varbinary(max) |Conteúdo do artefato de arquivo de biblioteca externa. |
|Plataforma |TINYINT |ID da plataforma do host no qual o SQL Server está instalado. |
|platform_desc | nvarchar(60) |Nome da plataforma do host. Os valores válidos são 'WINDOWS', 'LINUX'. |

### <a name="see-also"></a>Confira também  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CRIAR A BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
[Pacote de gerenciamento para o serviço do SQL Server Machine Learning](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
