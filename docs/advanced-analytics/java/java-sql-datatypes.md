---
title: Tipos de dados do Java com suporte no SQL Server 2019 | Microsoft Docs
description: Mapear tipos de dados do Java para o SQL Server para estruturas de dados de entrada e saída e parâmetros de entrada na sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3510b53510514daa125382fc10ea33285fe44a80
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46714868"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java e o SQL Server com suporte a tipos de dados

Este artigo mapeia tipos de dados do SQL Server para tipos de dados do Java para estruturas de dados e parâmetros em [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

## <a name="data-types-for-data-sets"></a>Tipos de dados para conjuntos de dados

Atualmente, há suporte para os seguintes tipos de dados SQL e o Java para conjuntos de dados de entrada e saída.

| Tipo SQL        | Tipo de Java | | |
| ------------- |-------------|-|-|
| bit      | booleano | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | Cadeia de caracteres (unicode)      | | |
| nvarchar (n) | Cadeia de caracteres (unicode)      | | |
| binary(n) | byte[]      | | |
| varbinary (n) | byte[]      | | |

## <a name="data-types-for-input-parameters"></a>Tipos de dados para parâmetros de entrada

Atualmente, há suporte para os seguintes tipos de dados SQL e o Java para parâmetros de entrada.

| Tipo SQL        | Tipo de Java | | |
| ------------- |-------------|-|-|
| bit      | booleano | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | Cadeia de caracteres (unicode)      | | |
| nvarchar (n) | Cadeia de caracteres (unicode)      | | |
| binary(n) | byte[]      | | |
| varbinary (n) | byte[]      | | |
| nvarchar(max) | Cadeia de caracteres (unicode)      | | |
| varbinary(max) | byte[]      | | |

## <a name="see-also"></a>Confira também

+ [Como chamar o Java no SQL Server](howto-call-java-from-sql.md)
+ [Exemplo de Java no SQL Server](java-first-sample.md)
+ [Extensão da linguagem Java no SQL Server](extension-java.md)