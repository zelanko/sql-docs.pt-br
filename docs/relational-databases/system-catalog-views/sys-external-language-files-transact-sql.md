---
title: sys.external_language_files (Transact-SQL) – SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: dphansen
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
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0d1325311ef0b708f5a3abd5f4494e099863efc2
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65995084"
---
# <a name="sysexternallanguagefiles-transact-sql"></a>sys.external_language_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este modo de exibição de catálogo fornece uma lista dos arquivos de extensão de linguagem externo no banco de dados. **R** e **Python** são nomes reservados e nenhum idioma externo pode ser criado com esses nomes específicos.

Quando uma linguagem externa é criada a partir de um file_spec, a extensão em si e suas propriedades são listadas nesta exibição. Essa exibição contém uma entrada por idioma, por sistema operacional.

## <a name="sysexternallanguages"></a>sys.external_languages

O sys.external_language_files do modo de exibição de catálogo lista uma linha para cada extensão de linguagem externo no banco de dados. Parâmetros

|Nome da coluna |Tipo de dados | Descrição|
|------|------|------|
|external_language_id |INT | Identificação do idioma externo|
|content|varbinary(max) |Conteúdo do arquivo de extensão de linguagem externo|
|file_name|nvarchar(266)|Nome do arquivo de extensão de linguagem|
|Plataforma|TINYINT|ID da plataforma do host no qual o SQL Server está instalado|
|platform_desc |nvarchar(60)|Nome da plataforma do host. Os valores válidos são 'WINDOWS', 'LINUX'.|
|parameters|nvarchar(4000)|Prameters de idiomas externos|
|environment_variables |nvarchar(4000)|Variáveis de ambiente de linguagem externo|

## <a name="see-also"></a>Confira também  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [CRIAR IDIOMA EXTERNO](../../t-sql/statements/create-external-language-transact-sql.md)  
