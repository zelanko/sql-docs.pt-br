---
title: sys. external_library_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
ms.prod: sql
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: a7f6038f9929d1220d3fb272ce3bdd9aa726a551
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173572"
---
# <a name="sysexternal_library_files-transact-sql"></a>sys.external_library_files (Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Lista uma linha para cada arquivo que compõe uma biblioteca externa.

|Nome da coluna |Tipo de dados |Descrição|
|------|------|-----|
|external_library_id | INT |ID do objeto da biblioteca externa. |
|conteúdo |varbinary(max) |Conteúdo do artefato do arquivo da biblioteca externa. |
|plataforma |TINYINT |ID da plataforma de host na qual o SQL Server está instalado. |
|platform_desc | nvarchar(60) |Nome da plataforma do host. Os valores válidos são ' WINDOWS ', ' LINUX '. |

### <a name="see-also"></a>Confira também  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CRIAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
