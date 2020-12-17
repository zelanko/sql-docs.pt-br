---
title: Converter tipos de dados do Python e do SQL
description: Examine as conversões implícita e explícita de tipo de dados entre o Python e SQL Server em soluções de ciência de dados e de aprendizado de máquina.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/06/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: cadb382861d868a96319483cbc54e847093fbe17
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471037"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Mapeamentos de tipo de dados entre o Python e o SQL Server
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Este artigo lista os tipos de dados compatíveis e as conversões de tipo de dados executadas ao usar o recurso de integração do Python nos Serviços de Machine Learning do SQL Server.

O Python dá suporte a um número limitado de tipos de dados em comparação com o SQL Server. Como resultado, sempre que você usar dados do SQL Server em scripts Python, os dados SQL poderão ser convertidos implicitamente em um tipo de dados Python compatível. No entanto, geralmente uma conversão exata não pode ser executada de modo automático e um erro é retornado.

## <a name="python-and-sql-data-types"></a>Tipos de dados do SQL e do Python

Esta tabela lista as conversões implícitas que são fornecidas. Nenhum outro tipo de dados é compatível.

| Tipo SQL             | Tipo do Python | Descrição |
|----------------------|-------------|-------------|
| **bigint**           | `float64`   |
| **binary**           | `bytes`     |
| **bit**              | `bool`      |
| **char**             | `str`       |
| **date**             | `datetime`  |
| **datetime**         |`datetime`   | Compatível com o SQL Server 2017 CU6 e versões superiores (com matrizes **NumPy** do tipo `datetime.datetime` ou **Pandas** `pandas.Timestamp`). O `sp_execute_external_script` agora é compatível com tipos `datetime` com segundos fracionários.|
| **float**            | `float64`   |
| **nchar**            | `str`       |
| **nvarchar**         | `str`       |
| **nvarchar(max)**    | `str`       |
| **real**             | `float64`   |
| **smalldatetime**    | `datetime`  |
| **smallint**         | `int32`     |
| **tinyint**          | `int32`     |
| **uniqueidentifier** | `str`       |
| **varbinary**        | `bytes`     |
| **varbinary(max)**   | `bytes`     |
| **varchar(n)**       | `str`       |
| **varchar(max)**     | `str`       |

## <a name="see-also"></a>Veja também

+ [Mapeamentos de tipo de dados entre o R e o SQL Server](../r/r-libraries-and-data-types.md)
