---
title: sys.external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
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
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 78923a0eb1404c1437c6e1144888261e542ebc5a
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471108"
---
# <a name="sysexternallibraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Dá suporte ao gerenciamento de bibliotecas de pacotes relacionadas a tempos de execução externos, como R, Python e Java.

> [!NOTE]
> No SQL Server 2017, há compatibilidade apenas com a linguagem R e a plataforma Windows. Há suporte para R, Python e Java nas plataformas Windows e Linux no SQL Server 2019 CTP 2.4.

## <a name="sysexternallibraries"></a>sys.external_libraries

A exibição de catálogo sys. external_libraries lista uma linha para cada biblioteca externa que foi carregada no banco de dados.

|Nome da coluna |Tipo de dados | Descrição|
|------|------|------|
|external_library_id |int | ID do objeto da biblioteca externa. |
|name |sysname |Nome da biblioteca externa. É exclusivo dentro do banco de dados por proprietário.|
|principal_id |int |ID da entidade de segurança que possui essa biblioteca externa. |
|language | sysname | Nome do idioma ou tempo de execução que dá suporte à biblioteca externa. Os valores válidos são ' R ', ' Python ' e ' Java '. Tempos de execução adicionais podem ser adicionados no futuro.|
|scope |int |0 para escopo público; 1 para escopo privado |  
|scope_desc |varchar(7) |Indica se o pacote é público ou privado|

## <a name="see-also"></a>Confira também  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CRIAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Instalar os novos pacotes R no SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)  
+ [Instalar os novos pacotes Python no SQL Server](../../advanced-analytics/python/install-additional-python-packages-on-sql-server.md)  