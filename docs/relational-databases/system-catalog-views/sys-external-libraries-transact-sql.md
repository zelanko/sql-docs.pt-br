---
title: sys.external_libraries (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
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
ms.openlocfilehash: 6b1bfc00b403fa76f692db78593ed4c0e6b53ce8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664431"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Suporta o gerenciamento de bibliotecas de pacotes relacionadas a runtimes externos, como R, Python e Java.

> [!NOTE]
> No SQL Server 2017, há compatibilidade apenas com a linguagem R e a plataforma Windows. Há suporte para R, Python e Java nas plataformas Windows e Linux no SQL Server 2019 e posteriores.

## <a name="sysexternal_libraries"></a>sys.external_libraries

O catálogo view sys.external_libraries lista uma linha para cada biblioteca externa que foi carregada no banco de dados.

|Nome da coluna |Tipo de dados | Descrição|
|------|------|------|
|external_library_id |INT | ID do objeto da biblioteca externa. |
|name |sysname |Nome da biblioteca externa. É único dentro do banco de dados por proprietário.|
|principal_id |INT |ID do diretor que possui esta biblioteca externa. |
|Linguagem | sysname | Nome do idioma ou tempo de execução que suporta a biblioteca externa. Os valores válidos são 'R', 'Python' e 'Java'. Tempos adicionais podem ser adicionados no futuro.|
|scope |INT |0 para escopo público; 1 para escopo privado |  
|scope_desc |varchar(7) |Indica se o pacote é público ou privado|

## <a name="see-also"></a>Confira também  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [CRIAR BIBLIOTECA EXTERNA](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Instalar os novos pacotes R no SQL Server](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [Instalar os novos pacotes Python no SQL Server](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  