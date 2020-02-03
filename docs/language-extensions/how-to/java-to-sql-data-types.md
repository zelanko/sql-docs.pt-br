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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
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
| nchar(n) | String      | | |
| nvarchar(n) | String      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | String      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | String | | |
| char(n) | String | Há suporte apenas para cadeias de caracteres UTF8 | |
| varchar(n) | String | Há suporte apenas para cadeias de caracteres UTF8 | |
| varchar(max) | String | Há suporte apenas para cadeias de caracteres UTF8 | |
| date | java.sql.date  | | |
| numeric | java.math.BigDecimal  | | |
| decimal | java.math.BigDecimal  | | |
| money | java.math.BigDecimal  | | |
| SMALLMONEY | java.math.BigDecimal  | | |
| smalldatetime | java.sql.timestamp  | | |
| DATETIME | java.sql.timestamp  | | |
| datetime2 | java.sql.timestamp  | | |


## <a name="next-steps"></a>Próximas etapas

+ [Como chamar Java no SQL Server](../how-to/call-java-from-sql.md)
