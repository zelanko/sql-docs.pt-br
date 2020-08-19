---
description: sys. external_languages (Transact-SQL)-SQL Server
title: sys. external_languages (Transact-SQL)-SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_languages
- external_languages_TSQL
- sys.external_languages
- sys.external_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_languages catalog view
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1f44ce24baf72b5bb93e8d649d8fa4ebed1d6e99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420120"
---
# <a name="sysexternal_languages-transact-sql"></a>sys. external_languages (Transact-SQL)
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

Essa exibição de catálogo fornece uma lista dos idiomas externos no banco de dados. **R** e **Python** são nomes reservados, e nenhuma linguagem externa pode ser criada com esses nomes específicos.

## <a name="sysexternal_languages"></a>sys.external_languages

A exibição de catálogo sys. external_languages lista uma linha para cada idioma externo no banco de dados.

|Nome da coluna |Tipo de dados | Descrição|
|------|------|------|
|external_language_id |INT | ID do idioma externo|
|Linguagem |sysname |Nome do idioma externo. É exclusiva no banco de dados. R e Python são nomes reservados por instância|
|create_date |datetime2 |Data e hora da criação|
|principal_id |INT |ID da entidade de segurança que pertence a esta biblioteca externa|

## <a name="see-also"></a>Confira também  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [CRIAR IDIOMA EXTERNO](../../t-sql/statements/create-external-language-transact-sql.md) 
