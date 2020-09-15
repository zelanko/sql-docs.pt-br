---
title: Converter tipos de dados do Python e do SQL
description: Examine as conversões implícita e explícita de tipo de dados entre o Python e SQL Server em soluções de ciência de dados e de aprendizado de máquina.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/30/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ee493ec09c5cfc8a5198239cd5cafcb2579f50d8
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178606"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Mapeamentos de tipo de dados entre o Python e o SQL Server
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

Para soluções do Python executadas no recurso de integração do Python nos Serviços de Machine Learning do SQL Server, examine a lista de tipos de dados não compatíveis e as conversões de tipo de dados que podem ser executadas implicitamente quando os dados são passados entre o Python e o SQL Server.

## <a name="python-version"></a>Versão do Python

Um subconjunto da funcionalidade RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees e talvez alguns outros) é fornecido usando APIs do Python, usando um novo pacote **revoscalepy** do Python. Você pode usar este pacote para trabalhar usando dados por meio das estruturas de dados do Pandas, arquivos XDF ou consultas de dados SQL.

Para obter mais informações, confira o [módulo revoscalepy no SQL Server](ref-py-revoscalepy.md) e a [referência de função revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

O Python dá suporte a um número limitado de tipos de dados em comparação com o SQL Server. Como resultado, sempre que você usar dados do SQL Server em scripts Python, os dados poderão ser convertidos implicitamente em um tipo de dados compatível. No entanto, geralmente uma conversão exata não pode ser executada automaticamente e um erro é retornado.

## <a name="python-and-sql-data-types"></a>Tipos de dados do SQL e do Python

Esta tabela lista as conversões implícitas que são fornecidas. Nenhum outro tipo de dados é compatível.

|SQLtype|Tipo do Python|Descrição
|-------|-----------|---------------------------------------------------------------------------------------------|
|**bigint**|`float64`|
|**binary**|`bytes`|
|**bit**|`bool`|
|**char**|`str`|
|**date**|`datetime`|
|**datetime**|`datetime`|Compatível com o SQL Server 2017 CU6 e versões superiores (com matrizes **NumPy** do tipo `datetime.datetime` ou **Pandas** `pandas.Timestamp`). O `sp_execute_external_script` agora é compatível com tipos `datetime` com segundos fracionários.|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float64`|
|**smalldatetime**|`datetime`|
|**smallint**|`int32`|
|**tinyint**|`int32`|
|**uniqueidentifier**|`str`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**varchar(max)**|`str`|
