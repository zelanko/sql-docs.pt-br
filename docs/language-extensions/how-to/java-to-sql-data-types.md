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
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: d5703470849f627cca87c471ea666b7c1b0e7e85
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471737"
---
# <a name="java-and-sql-server-supported-data-types"></a>Tipos de dados com suporte no Java e SQL Server
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Este artigo mapeia tipos de dados do SQL Server para tipos de dados Java para estruturas de dados e parâmetros em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

No momento, há suporte para os tipos de dados SQL e Java a seguir para conjuntos de dados de Entrada/Saída e parâmetros de Entrada/Saída.

| Tipo de dados SQL        | Tipo de dados Java | Comentário |
| ------------- |-------------|-|
| bit      | booleano | |
| Tinyint      | short      | |
| Smallint | short      | |
| Int | INT      | |
| Real | FLOAT      | |
| Bigint | long      | |
| FLOAT | double      | |
| nchar(n) | String      | |
| nvarchar(n) | String      | |
| binary(n) | byte[]      | |
| varbinary(n) | byte[]      | |
| nvarchar(max) | String      | |
| varbinary(max) | byte[]      | |
| UNIQUEIDENTIFIER | String | |
| char(n) | String | Há suporte apenas para cadeias de caracteres UTF8 |
| varchar(n) | String | Há suporte apenas para cadeias de caracteres UTF8 |
| varchar(max) | String | Há suporte apenas para cadeias de caracteres UTF8 |
| date | java.sql.date  | |
| numeric | java.math.BigDecimal  | |
| decimal | java.math.BigDecimal  | |
| money | java.math.BigDecimal  | |
| SMALLMONEY | java.math.BigDecimal  | |
| smalldatetime | java.sql.timestamp  | |
| DATETIME | java.sql.timestamp  | |
| datetime2 | java.sql.timestamp  | |


## <a name="next-steps"></a>Próximas etapas

+ [Como chamar Java no SQL Server](../how-to/call-java-from-sql.md)