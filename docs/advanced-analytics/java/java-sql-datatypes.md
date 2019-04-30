---
title: Tipos de dados do Java com suporte no SQL Server 2019 – extensões de linguagem do SQL Server
description: Mapear tipos de dados do Java para o SQL Server para estruturas de dados de entrada e saída e parâmetros de entrada na sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 14a2bc5594b16610dfb8278ab82a9e7b8b22fea6
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473598"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java e o SQL Server com suporte a tipos de dados

Este artigo mapeia tipos de dados do SQL Server para tipos de dados do Java para estruturas de dados e parâmetros em [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

## <a name="data-types-for-data-sets"></a>Tipos de dados para conjuntos de dados

Atualmente, há suporte para os seguintes tipos de dados SQL e o Java para conjuntos de dados de entrada e saída.


| Tipo de dados SQL        | Tipo de dados Java | Comentário | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | Cadeia de caracteres      | | |
| nvarchar(n) | Cadeia de caracteres      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | Cadeia de caracteres      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | Cadeia de caracteres | | |
| char(n) | Cadeia de caracteres | Somente UTF8 cadeias de caracteres com suporte | |
| varchar(n) | Cadeia de caracteres | Somente UTF8 cadeias de caracteres com suporte | |
| varchar(max) | Cadeia de caracteres | Somente UTF8 cadeias de caracteres com suporte | |

## <a name="data-types-for-input-parameters"></a>Tipos de dados para parâmetros de entrada

Atualmente, há suporte para os seguintes tipos de dados SQL e o Java para parâmetros de entrada.

| Tipo de dados SQL        | Tipo de dados Java | Comentário | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | Cadeia de caracteres      | | |
| nvarchar(n) | Cadeia de caracteres      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | Cadeia de caracteres      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | Cadeia de caracteres | | |
| char(n) | Cadeia de caracteres | Somente UTF8 cadeias de caracteres com suporte | |
| varchar(n) | Cadeia de caracteres | Somente UTF8 cadeias de caracteres com suporte | |
| varchar(max) | Cadeia de caracteres | Somente UTF8 cadeias de caracteres com suporte | |

## <a name="next-steps"></a>Próximas etapas

+ [Como chamar o Java no SQL Server](howto-call-java-from-sql.md)
+ [Exemplo de Java no SQL Server](java-first-sample.md)
+ [Extensão da linguagem Java no SQL Server](extension-java.md)
