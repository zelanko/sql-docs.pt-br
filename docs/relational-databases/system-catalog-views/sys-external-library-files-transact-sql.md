---
title: sys.external_library_files (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- external_library_files
- external_library_files_TSQL
- sys.external_library_files
- sys.external_library_files_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.external_library_files catalog view
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: a3196218bbb886544a77c2fd1184c806591b16e6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysexternallibraryfiles-transact-sql"></a>sys.external_library_files (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Lista uma linha para cada arquivo que compõe uma biblioteca externa.

|Nome da coluna |Tipo de dados |Description|
|------|------|-----|
|external_library_id | int |ID do objeto de biblioteca externa. |
|content |varbinary(max) |Conteúdo do artefato de arquivo de biblioteca externa. |
|Plataforma |tinyint |ID da plataforma de host no qual o SQL Server está instalado. |
|platform_desc | nvarchar(60) |Nome da plataforma de host. Os valores válidos são 'WINDOWS', 'LINUX'. |

### <a name="see-also"></a>Consulte também  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CRIAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
[Gerenciamento de pacotes para serviço de aprendizado de máquina do SQL Server](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
