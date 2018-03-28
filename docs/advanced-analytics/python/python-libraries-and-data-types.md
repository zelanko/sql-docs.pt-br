---
title: Bibliotecas de Python | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 14691885d6dcdb91558ddc9566f4320c8119a9dd
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="python-libraries-and-data-types"></a>Bibliotecas de Python e tipos de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve as bibliotecas do Python que estão incluídas com os seguintes produtos:

+ Serviços (no banco de dados) de aprendizado de máquina do SQL Server
+ Server (autônomo) de aprendizado de máquina da Microsoft

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



