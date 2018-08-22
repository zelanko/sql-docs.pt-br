---
title: Tipos de dados e bibliotecas do Python no SQL Server Machine Learning | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7b977d079589dbb4c54d5c31fec644d9f984dd61
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "40434846"
---
# <a name="python-libraries-and-data-types"></a>Bibliotecas Python e tipos de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve as bibliotecas de Python que estão incluídas com serviços do SQL Server Machine Learning (no banco de dados) e instalações (autônomo).

Este artigo também lista os tipos de dados sem suporte e lista os dados de conversões de tipo que podem ser executadas implicitamente quando dados são passados entre Python e o SQL Server.

## <a name="python-version"></a>Versão do Python

Distribuição do SQL Server 2017 Anaconda 4.2 e Python 3.6.

Um subconjunto da funcionalidade de RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, talvez alguns outros) é fornecida usando as APIs do Python, usando um novo pacote do Python **revoscalepy**. Você pode usar esse pacote para trabalhar com dados usando consultas de dados SQL, arquivos XDF ou quadros de dados Pandas.

Para obter mais informações, consulte [What ' s revoscalepy?](what-is-revoscalepy.md).

## <a name="python-and-sql-data-types"></a>Python e tipos de dados SQL

Python dá suporte a um número limitado de tipos de dados em comparação com o SQL Server.

Como resultado, sempre que você usar dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em scripts de Python, dados podem ser convertidos implicitamente em um tipo de dados compatíveis. No entanto, muitas vezes uma conversão exata não pode ser executada automaticamente e um erro será retornado.

Esta tabela lista as conversões implícitas que são fornecidas. Não há suporte para outros tipos de dados.

|SQLtype|Tipo de Python|
|-|-|
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



