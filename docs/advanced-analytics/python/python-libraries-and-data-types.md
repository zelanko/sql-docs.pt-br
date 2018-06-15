---
title: Tipos de dados e bibliotecas de Python no aprendizado de máquina do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f8dfa7f343a3a179b05b624a083238e08011c4a5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31201688"
---
# <a name="python-libraries-and-data-types"></a>Tipos de dados e bibliotecas do Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve as bibliotecas do Python que são incluídas no serviços de aprendizado de máquina do SQL Server (no banco de dados) e instalações (autônomo).

Este artigo também lista os tipos de dados sem suporte e lista o tipo de dados conversões que podem ser realizadas implicitamente quando dados são passados entre Python e SQL Server.

## <a name="python-version"></a>Versão do Python

SQL Server 2017 CTP 2.0 inclui uma parte da distribuição Anaconda e Python 3.6.

Um subconjunto da funcionalidade RevoScaleR (rxLinMod, rxLogit, rxPredict, rxDTrees, rxBTrees, talvez alguns outros) é fornecido usando APIs do Python, usando um novo pacote do Python **revoscalepy**. Você pode usar esse pacote para trabalhar com dados usando consultas de dados SQL, arquivos XDF ou quadros de dados Pandas.

Para obter mais informações, consulte [revoscalepy novidades?](what-is-revoscalepy.md).

## <a name="python-and-sql-data-types"></a>Python e tipos de dados SQL

Python dá suporte a um número limitado de tipos de dados em comparação com o SQL Server.

Como resultado, sempre que você usar dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em scripts de Python, dados podem ser convertidos implicitamente em um tipo de dados compatíveis. No entanto, geralmente uma conversão exata não pode ser executada automaticamente e um erro será retornado.

Esta tabela lista as conversões implícitas que são fornecidas. Não há suporte para outros tipos de dados.

|SQLtype|Tipo de Python|
|-|-|
|**bigint**|`numeric`|
|**binary**|`raw`|
|**bit**|`bool`|
|**char**|`str`|
|**float**|`float64`|
|**Int**|`int32`|
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



