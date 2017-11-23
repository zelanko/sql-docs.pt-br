---
title: sys.external_libraries (Transact-SQL) | Microsoft Docs
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
- external_libraries
- external_libraries_TSQL
- sys.external_libraries
- sys.external_libraries_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.external_libraries catalog view
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: bb229022bcccfb9cdc8c419844d30335337575d4
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]


Dá suporte ao gerenciamento de bibliotecas de pacote relacionadas a tempos de execução externos, como R ou Python.

## <a name="sysexternallibraries"></a>sys.external_libraries

O sys.external_libraries de exibição de catálogo lista uma linha para cada biblioteca externa que tenha sido carregada no banco de dados.

|Nome da coluna |Tipo de dados | Description|
|------|------|------|
|external_library_id |int | ID do objeto de biblioteca externa. |
|name |sysname |Nome da biblioteca externa. É exclusivo no banco de dados por proprietário.|
|principal_id |int |ID da entidade de segurança que possui esta biblioteca externa. |
|language | sysname | Nome do idioma ou tempo de execução que oferece suporte a biblioteca externa. Os valores válidos são 'R'. Tempos de execução adicionais podem ser adicionados no futuro.|
|escopo |int |0 para escopo público. 1 para o escopo particular |  
|scope_desc |varchar(7) |Indica se o pacote é público ou privado|


## <a name="see-also"></a>Consulte também  
[sys.external_library_files](sys-external-library-files-transact-sql.md)  
[CRIAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
[Gerenciamento de pacotes do SQL Server R Services](../../advanced-analytics/r/installing-and-managing-r-packages.md)  
