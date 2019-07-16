---
title: Conversões - aprendizagem de máquina do SQL Server de tipo de dados do Python para SQL
description: Examine os tipo de dados implícitas e explícitas converstions entre Python e o SQL Server em soluções de aprendizado de máquina e ciência de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 652824e4b038e629cf9b998dd6fae64465426d0b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962765"
---
# <a name="data-type-mappings-between-python-and-sql-server"></a>Mapeamentos de tipo de dados entre o Python e o SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Para soluções de Python que executam o recurso de integração de Python em serviços do SQL Server Machine Learning, examine a lista de tipos de dados sem suporte e as conversões de tipo de dados que podem ser executadas implicitamente quando dados são passados entre Python e o SQL Server.

## <a name="python-version"></a>Versão do Python

Distribuição do SQL Server 2017 Anaconda 4.2 e Python 3.6.

Um subconjunto da funcionalidade de RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, talvez alguns outros) é fornecida usando as APIs do Python, usando um novo pacote do Python **revoscalepy**. Você pode usar esse pacote para trabalhar com dados usando consultas de dados SQL, arquivos XDF ou quadros de dados Pandas.

Para obter mais informações, consulte [módulo revoscalepy no SQL Server](ref-py-revoscalepy.md) e [referência de função revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package).

Python dá suporte a um número limitado de tipos de dados em comparação com o SQL Server. Como resultado, sempre que você usa dados do SQL Server em scripts de Python, dados podem ser implicitamente convertidos em um tipo de dados compatíveis. No entanto, muitas vezes uma conversão exata não pode ser executada automaticamente e um erro será retornado.

## <a name="python-and-sql-data-types"></a>Python e tipos de dados SQL

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

