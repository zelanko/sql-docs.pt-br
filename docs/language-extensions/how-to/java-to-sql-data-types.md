---
title: Tipos de dados Java
titleSuffix: SQL Server Language Extensions
description: Mapeie os tipos de dados do Java para o SQL Server para estruturas de dados de entrada e saída e para parâmetros de entrada no sp_execute_external_script.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d1df57079acd79fc5370d0f2f198dc2d624d6983
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658832"
---
# <a name="java-and-sql-server-supported-data-types"></a>Tipos de dados com suporte no Java e SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo mapeia tipos de dados do SQL Server para tipos de dados Java para estruturas de dados e parâmetros em [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

No momento, há suporte para os tipos de dados SQL e Java a seguir para conjuntos de dados de Entrada/Saída e parâmetros de Entrada/Saída.

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
| char(n) | Cadeia de caracteres | Há suporte apenas para cadeias de caracteres UTF8 | |
| varchar(n) | Cadeia de caracteres | Há suporte apenas para cadeias de caracteres UTF8 | |
| varchar(max) | Cadeia de caracteres | Há suporte apenas para cadeias de caracteres UTF8 | |
| Data | java.sql.date  | | |
| NUMERIC | java.math.BigDecimal  | | |
| Decimal | java.math.BigDecimal  | | |
| money | java.math.BigDecimal  | | |
| SMALLMONEY | java.math.BigDecimal  | | |
| smalldatetime | java.sql.timestamp  | | |
| DATETIME | java.sql.timestamp  | | |
| datetime2 | java.sql.timestamp  | | |


## <a name="next-steps"></a>Próximas etapas

+ [Como chamar Java no SQL Server](../how-to/call-java-from-sql.md)
