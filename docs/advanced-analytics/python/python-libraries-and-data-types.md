---
title: Converter tipos de dados do Python e do SQL
description: Examine as conversões implícita e explícita de tipo de dados entre o Python e SQL Server em soluções de ciência de dados e de aprendizado de máquina.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f22f838bc78d4791e73a1d107cd253aae314d205
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73727522"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Mapeamentos de tipo de dados entre o Python e o SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Para soluções do Python executadas no recurso de integração do Python nos Serviços de Machine Learning do SQL Server, examine a lista de tipos de dados não compatíveis e as conversões de tipo de dados que podem ser executadas implicitamente quando os dados são passados entre o Python e o SQL Server.

## <a name="python-version"></a>Versão do Python

Um subconjunto da funcionalidade RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees e talvez alguns outros) é fornecido usando APIs do Python, usando um novo pacote **revoscalepy** do Python. Você pode usar este pacote para trabalhar usando dados por meio das estruturas de dados do Pandas, arquivos XDF ou consultas de dados SQL.

Para obter mais informações, confira o [módulo revoscalepy no SQL Server](ref-py-revoscalepy.md) e a [referência de função revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

O Python dá suporte a um número limitado de tipos de dados em comparação com o SQL Server. Como resultado, sempre que você usar dados do SQL Server em scripts Python, os dados poderão ser convertidos implicitamente em um tipo de dados compatível. No entanto, geralmente uma conversão exata não pode ser executada automaticamente e um erro é retornado.

## <a name="python-and-sql-data-types"></a>Tipos de dados do SQL e do Python

Esta tabela lista as conversões implícitas que são fornecidas. Nenhum outro tipo de dados é compatível.

|SQLtype|Tipo do Python|
|-------|-----------|
|**bigint**|`numeric`|
|**binary**|`raw`|
|**bit**|`bool`|
|**char**|`str`|
|**float**|`float64`|
|**int**|`int32`|
|**nchar**|`str`|
|**nvarchar**|`str`|
|**nvarchar(max)**|`str`|
|**real**|`float32`|
|**smallint**|`int16`|
|**tinyint**|`uint8`|
|**varbinary**|`bytes`|
|**varbinary(max)**|`bytes`|
|**varchar(n)**|`str`|
|**varchar(max)**|`str`|
