---
title: Conversões de tipo de dados de Python para SQL
description: Examine o tipo de dados implícito e explícito converstions entre Python e SQL Server em soluções de ciência de dados e de aprendizado de máquina.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 043a27cc53c2dca955eb0bea1ed07433bc9183b8
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345511"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Mapeamentos de tipo de dados entre Python e SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Para soluções de Python executadas no recurso de integração do Python no SQL Server Serviços de Machine Learning, examine a lista de tipos de dados sem suporte e conversões de tipo de dados que podem ser executadas implicitamente quando os dados são passados entre Python e SQL Server.

## <a name="python-version"></a>Versão do Python

SQL Server 2017 Anaconda 4,2 Distribution e Python 3,6.

Um subconjunto da funcionalidade RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, talvez alguns outros) é fornecido usando APIs do Python, usando um novo pacote Python **revoscalepy**. Você pode usar este pacote para trabalhar com dados usando os quadros de dados pandas, arquivos XDF ou consultas de dados SQL.

Para obter mais informações, consulte [módulo revoscalepy em](ref-py-revoscalepy.md) [referência de função](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)SQL Server e revoscalepy.

O Python dá suporte a um número limitado de tipos de dados em comparação com SQL Server. Como resultado, sempre que você usar dados de SQL Server em scripts Python, os dados poderão ser convertidos implicitamente em um tipo de dados compatível. No entanto, geralmente uma conversão exata não pode ser executada automaticamente e um erro é retornado.

## <a name="python-and-sql-data-types"></a>Tipos de dados do Python e do SQL

Esta tabela lista as conversões implícitas que são fornecidas. Não há suporte para outros tipos de dados.

|SQLtype|Tipo de Python|
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

## <a name="see-also"></a>Confira também

