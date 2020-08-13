---
title: sys. external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
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
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: b6a24a142deef2283c58e21941293f31479f997b
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88180067"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Dá suporte ao gerenciamento de bibliotecas de pacotes relacionadas a tempos de execução externos, como R, Python e Java.

> [!NOTE]
> No SQL Server 2017, há compatibilidade apenas com a linguagem R e a plataforma Windows. Há suporte para R, Python e Java nas plataformas Windows e Linux no SQL Server 2019 e posteriores. No Azure SQL Instância Gerenciada, R e Python têm suporte.

## <a name="sysexternal_libraries"></a>sys.external_libraries

A exibição de catálogo sys. external_libraries lista uma linha para cada biblioteca externa que foi carregada no banco de dados.

|Nome da coluna |Tipo de dados | Descrição|
|------|------|------|
|external_library_id |INT | ID do objeto da biblioteca externa. |
|name |sysname |Nome da biblioteca externa. É exclusivo dentro do banco de dados por proprietário.|
|principal_id |INT |ID da entidade de segurança que possui essa biblioteca externa. |
|Linguagem | sysname | Nome do idioma ou tempo de execução que dá suporte à biblioteca externa. Os valores válidos são ' R ', ' Python ' e ' Java '. Tempos de execução adicionais podem ser adicionados no futuro.|
|escopo |INT |0 para escopo público; 1 para escopo privado |  
|scope_desc |varchar (7) |Indica se o pacote é público ou privado|

## <a name="see-also"></a>Confira também  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CRIAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Instalar os novos pacotes R](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [Instalar os novos pacotes Python](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  