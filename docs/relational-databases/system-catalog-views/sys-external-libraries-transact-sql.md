---
title: sys.external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- external_libraries
- external_libraries_TSQL
- sys.external_libraries
- sys.external_libraries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_libraries catalog view
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1373849201dccbb36f7096549d63864a23330f14
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43075869"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


Dá suporte ao gerenciamento de bibliotecas de pacotes relacionados a tempos de execução externos, como R ou Python.

## <a name="sysexternallibraries"></a>sys.external_libraries

O sys.external_libraries do modo de exibição de catálogo lista uma linha para cada biblioteca externa que tenha sido carregada no banco de dados.

|Nome da coluna |Tipo de dados | Description|
|------|------|------|
|external_library_id |INT | ID do objeto de biblioteca externa. |
|nome |sysname |Nome da biblioteca externa. É exclusivo no banco de dados por proprietário.|
|principal_id |INT |ID da entidade de segurança que possui essa biblioteca externa. |
|language | sysname | Nome do idioma ou tempo de execução que dá suporte a biblioteca externa. Os valores válidos são 'R'. Tempos de execução adicionais podem ser adicionados no futuro.|
|escopo |INT |0 para um escopo público; 1 para o escopo particular |  
|scope_desc |varchar(7) |Indica se o pacote é pública ou privada|


## <a name="see-also"></a>Confira também  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[CRIAR A BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
[Pacote de gerenciamento para SQL Server R Services](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
