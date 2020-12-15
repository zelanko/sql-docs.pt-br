---
description: sys.external_language_files (Transact-SQL)-SQL Server
title: sys.external_language_files (Transact-SQL)-SQL Server | Microsoft Docs
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
monikerRange: '>=sql-server-ver15'
ms.openlocfilehash: f09590931848f963ebe62736d4a890c0cf11ed0d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477457"
---
# <a name="sysexternal_language_files-transact-sql"></a>sys.external_language_files (Transact-SQL)
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

Esta exibição de catálogo fornece uma lista dos arquivos de extensão de idioma externo no banco de dados. **R** e **Python** são nomes reservados, e nenhuma linguagem externa pode ser criada com esses nomes específicos.

Quando um idioma externo é criado a partir de um file_spec, a própria extensão e suas propriedades são listadas nessa exibição. Essa exibição conterá uma entrada por idioma, por sistema operacional.

## <a name="sysexternal_languages"></a>sys.external_languages

A exibição de catálogo sys.external_language_files lista uma linha para cada extensão de idioma externo no banco de dados. Parâmetros

|Nome da coluna |Tipo de dados | Descrição|
|------|------|------|
|external_language_id |INT | ID do idioma externo|
|conteúdo|varbinary(max) |Conteúdo do arquivo de extensão de idioma externo|
|file_name|nvarchar (266)|Nome do arquivo de extensão de idioma|
|plataforma|TINYINT|ID da plataforma de host na qual o SQL Server está instalado|
|platform_desc |nvarchar(60)|Nome da plataforma do host. Os valores válidos são ' WINDOWS ', ' LINUX '.|
|parâmetros|nvarchar(4000)|Prameters de idioma externo|
|environment_variables |nvarchar(4000)|Variáveis de ambiente de idioma externo|

## <a name="see-also"></a>Consulte também  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [CRIAR IDIOMA EXTERNO](../../t-sql/statements/create-external-language-transact-sql.md)  
