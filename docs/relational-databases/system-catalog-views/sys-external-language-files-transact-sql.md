---
title: sys. external_language_files (Transact-SQL)-SQL Server | Microsoft Docs
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
ms.openlocfilehash: a991761e26f8f63ae6431d7d242fb2625135d3ac
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627482"
---
# <a name="sysexternal_language_files-transact-sql"></a>sys. external_language_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Esta exibição de catálogo fornece uma lista dos arquivos de extensão de idioma externo no banco de dados. **R** e **Python** são nomes reservados, e nenhuma linguagem externa pode ser criada com esses nomes específicos.

Quando um idioma externo é criado a partir de um file_spec, a própria extensão e suas propriedades são listadas nessa exibição. Essa exibição conterá uma entrada por idioma, por sistema operacional.

## <a name="sysexternal_languages"></a>sys.external_languages

A exibição de catálogo sys. external_language_files lista uma linha para cada extensão de idioma externo no banco de dados. Parâmetros

|Nome da coluna |Tipo de dados | Descrição|
|------|------|------|
|external_language_id |INT | ID do idioma externo|
|conteúdo|varbinary(max) |Conteúdo do arquivo de extensão de idioma externo|
|file_name|nvarchar (266)|Nome do arquivo de extensão de idioma|
|plataforma|TINYINT|ID da plataforma de host na qual o SQL Server está instalado|
|platform_desc |nvarchar(60)|Nome da plataforma do host. Os valores válidos são ' WINDOWS ', ' LINUX '.|
|parâmetros|nvarchar(4000)|Prameters de idioma externo|
|environment_variables |nvarchar(4000)|Variáveis de ambiente de idioma externo|

## <a name="see-also"></a>Veja também  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [CRIAR IDIOMA EXTERNO](../../t-sql/statements/create-external-language-transact-sql.md)  
