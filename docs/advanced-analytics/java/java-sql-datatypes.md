---
title: Tipos de dados do Java com suporte no SQL Server 2019 - serviços do SQL Server Machine Learning
description: Mapear tipos de dados do Java para o SQL Server para estruturas de dados de entrada e saída e parâmetros de entrada na sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4c0f691b8bb389c2da2001d19f0684b7f928f707
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017812"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java e o SQL Server com suporte a tipos de dados

Este artigo mapeia tipos de dados do SQL Server para tipos de dados do Java para estruturas de dados e parâmetros em [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

## <a name="data-types-for-data-sets"></a>Tipos de dados para conjuntos de dados

Atualmente, há suporte para os seguintes tipos de dados SQL e o Java para conjuntos de dados de entrada e saída.

| Tipo de dados SQL        | Tipo de dados Java | Comentário | |
| ------------- |-------------|-|
| bit      | booleano | |
| Tinyint      | short      | |
| Smallint | short      | |
| Int | INT      | |
| Real | FLOAT      | |
| Bigint | long      | |
| FLOAT | double      | |
| nchar(n) | Cadeia de caracteres      | |
| nvarchar(n) | Cadeia de caracteres  | |
| binary(n) | byte[]      | |
| varbinary(n) | byte[]      | |
| nvarchar(max) | Cadeia de caracteres | |
| varbinary(max) | byte[] | |
| UNIQUEIDENTIFIER | Cadeia de caracteres | |
| char(n) | Cadeia de caracteres | Somente UTF8 cadeias de caracteres com suporte |
| varchar(n) | Cadeia de caracteres | Somente UTF8 cadeias de caracteres com suporte |
| varchar(max) | Cadeia de caracteres | Somente UTF8 cadeias de caracteres com suporte |

## <a name="data-types-for-input-parameters"></a>Tipos de dados para parâmetros de entrada

Atualmente, há suporte para os seguintes tipos de dados SQL e o Java para parâmetros de entrada.

| Tipo de dados SQL        | Tipo de dados Java | Comentário | |
| ------------- |-------------|-|-|
| bit      | booleano | | |
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

## <a name="see-also"></a>Confira também

+ [Como chamar o Java no SQL Server](howto-call-java-from-sql.md)
+ [Exemplo de Java no SQL Server](java-first-sample.md)
+ [Extensão da linguagem Java no SQL Server](extension-java.md)