---
title: sys.external_library_files (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.technology: system-objects
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
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a9666b58132feb79876c4e8074dc530440c05b2c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "68220341"
---
# <a name="sysexternallibraryfiles-transact-sql"></a>sys.external_library_files (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Lista uma linha para cada arquivo que compõe uma biblioteca externa.

|Nome da coluna |Tipo de dados |Descrição|
|------|------|-----|
|external_library_id | int |ID do objeto de biblioteca externa. |
|content |varbinary(max) |Conteúdo do artefato de arquivo de biblioteca externa. |
|Plataforma |TINYINT |ID da plataforma do host no qual o SQL Server está instalado. |
|platform_desc | nvarchar(60) |Nome da plataforma do host. Os valores válidos são 'WINDOWS', 'LINUX'. |

### <a name="see-also"></a>Confira também  

[sys.external_libraries](sys-external-libraries-transact-sql.md)  
[CRIAR A BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
[Pacote de gerenciamento para o serviço do SQL Server Machine Learning](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
