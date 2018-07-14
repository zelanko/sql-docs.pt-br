---
title: Formatos de data e hora | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- time data types [Integration Services]
- fast parse [Integration Services]
- date data types
- date and time formats for fast parse
ms.assetid: bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39
caps.latest.revision: 52
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d7c54b3ee399043d752efb9e55ce9c2f8fed488d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289382"
---
# <a name="date-and-time-formats"></a>Formatos de data e hora
  A análise rápida fornece um conjunto de rotinas simples e rápidas para analisar dados. A análise rápida oferece suporte aos seguintes formatos de tipos de dados de data e hora.  
  
## <a name="date-data-types"></a>Tipos de dados de data  
 A análise rápida oferece suporte aos seguintes formatos de cadeia de caracteres para dados de data:  
  
-   Formatos de data que incluem espaços em branco à esquerda. Por exemplo, o valor " 2004- 02-03" é válido.  
  
-   Os formatos ISO 8601, como listados na seguinte tabela:  
  
    |Formato|Description|  
    |------------|-----------------|  
    |AAAAMMDD<br /><br /> AAAA-MM-DD|Os formatos básico e estendido para um ano de quatro dígitos, um mês de dois dígitos e um dia de dois dígitos. No formato estendido, as datas são separadas por um hífen (-).|  
    |AAAA-MM|Os formatos básico e estendido de precisão reduzida para um ano de quatro dígitos e um mês de dois dígitos. No formato estendido, as datas são separadas por um hífen (-).|  
    |AAAA|O formato de precisão reduzida é um ano de quatro dígitos.|  
  
 A análise rápida não oferece suporte aos seguintes formatos para dados de data:  
  
-   Valores de meses alfabéticos. Por exemplo, o formato de data Oct-31-2003 não é válido.  
  
-   Formatos ambíguos como DD-MM-AAAA e MM-DD-AAAA. Por exemplo, as datas 03-04-1995 e 04-03-1995  não são válidas.  
  
-   Os formatos básico e estendido truncados para um ano de calendário de quatro dígitos e um dia de três dígitos em um ano, AAAADDD e AAAA-DDD.  
  
-   Os formatos básico e estendido para um ano de quatro dígitos, um número de dois dígitos para a semana do ano e um número de um dígito para o dia da semana, AAAASssD e AAAA-Sss-D.  
  
-   Os formatos básico e estendido truncados para uma data de um ano e semana são um ano de quatro dígitos e um número de dois dígitos para a semana, AAASss e AAAA-Sss.  
  
 A análise efetua a saída dos dados como DT_DBDATE. Os valores de data em formatos truncados são convertidos. Por exemplo, AAAA se torna AAAA0101.  
  
 Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
## <a name="time-data-type"></a>Tipo de dados de hora  
 A análise rápida oferece suporte aos seguintes formatos de cadeia de caracteres para dados de hora:  
  
-   Formatos de hora que incluem espaços em branco à esquerda. Por exemplo, o valor " 10:24" é válido.  
  
-   Formato de 24 horas. A análise rápida não oferece suporte à notação AM e PM.  
  
-   Os formatos de hora ISO 8601, como listados na seguinte tabela:  
  
    |Formato|Description|  
    |------------|-----------------|  
    |HHMISS<br /><br /> HH:MI:SS|Os formatos básico e estendido para uma hora de dois dígitos, um minuto de dois dígitos e um segundo de dois dígitos. No formato estendido, a hora é separada por dois pontos (:).|  
    |HHMI<br /><br /> HH:MI|Os formatos básico e estendido truncados para uma hora de dois dígitos e um minuto de dois dígitos. No formato estendido, a hora é separada por dois pontos (:).|  
    |HH|Formato truncado para uma hora de dois dígitos.|  
    |00:00:00<br /><br /> 000000<br /><br /> 0000<br /><br /> 00<br /><br /> 240000<br /><br /> 24:00:00<br /><br /> 2400<br /><br /> 24|O formato para meia-noite.|  
  
-   Os formatos de hora que especificam um fuso horário, como listados na seguinte tabela:  
  
    |Formato|Description|  
    |------------|-----------------|  
    |+HH:MI<br /><br /> +HHMI|Os formatos básico e estendido que indicam o número de horas e minutos que são adicionados ao tempo universal coordenado (UTC) para obter a hora local.|  
    |-HH:MI<br /><br /> -HHMI|Os formatos básico e estendido que indicam o número de horas e minutos que são subtraídos do UTC para obter a hora local.|  
    |+HH|O formato truncado que indica o número de horas que são adicionadas ao UTC para obter a hora local.|  
    |-HH|O formato truncado que indica o número de horas que são subtraídas do UTC para obter a hora local.|  
    |Z|Um valor 0 que indica a hora é representado no UTC.|  
  
     Os formatos para todos os dados de hora e data/hora podem incluir um elemento de fuso horário. Porém, o sistema ignora o valor do fuso horário, exceto quando os dados são do tipo DT_DBTIMESTAMPOFFSET. Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
     Nos formatos que incluem um elemento de fuso horário, não há espaço entre o elemento de hora e o de fuso horário, como mostrado no seguinte exemplo:  
  
     HH:MI:SS[+HH:MI]  
  
     As chaves no exemplo anterior indicam que o valor do fuso horário é opcional.  
  
-   Os formatos de hora que incluem uma fração decimal, como listados na seguinte tabela:  
  
    |Formato|Description|  
    |------------|-----------------|  
    |HH [.nnnnnnn]|n é um valor entre 0 e 9999999 que representa uma fração de horas. As chaves indicam que esse valor é opcional.<br /><br /> Por exemplo, o valor 12.750 indica 12:45.|  
    |HHMI [.nnnnnnn]<br /><br /> HH:MI [.nnnnnnn]|n é um valor entre 0 e 9999999 que representa uma fração de minutos. As chaves indicam que esse valor é opcional.<br /><br /> Por exemplo, o valor 1220.500 indica 12:20:30.|  
    |HHMISS [.nnnnnnn]<br /><br /> HH:MI:SS[.nnnnnnn]|n é um valor entre 0 e 9999999 que representa uma fração de segundos. As chaves indicam que esse valor é opcional.<br /><br /> Por exemplo, o valor 122040.250 indica 12:20:40.15.|  
  
    > [!NOTE]  
    >  O separador de fração para os formatos de hora na tabela anterior pode ser um decimal ou uma vírgula.  
  
-   Os valores de hora que incluem um segundo, como mostrado nos seguintes exemplos:  
  
     23:59:60[.0000000]  
  
     235960[.0000000]  
  
 A análise rápida efetua a saída de cadeias de caracteres como DT_DBTIME e DT_DBTIME2. Os valores de hora em formatos truncados são convertidos. Por exemplo, HH:MI se torna HH:MM:00 .000.  
  
 Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
## <a name="datetime-data-type"></a>Tipo de dados de data/hora  
 A análise rápida oferece suporte aos seguintes formatos de cadeia de caracteres para dados de data/hora:  
  
-   Formatos que incluem espaços em branco à esquerda. Por exemplo, o valor "  2003-01-10T203910" é válido.  
  
-   As combinações de formatos de data e de hora válidos separados por um T maiúsculo, e os formatos de fuso horário válidos, como AAAAMMDDT[HHMISS][+HH:MI]. Os valores de hora e de fuso horário não são obrigatórios. Por exemplo, "2003-10-14" são válidos.  
  
 A análise rápida não oferece suporte a intervalos de tempo. Por exemplo, um intervalo de tempo identificado por uma data e hora iniciais e finais no formato AAAAMMDDThhmmss/AAAAMMDDThhmmss não pode ser analisado.  
  
 A análise rápida efetua saídas das cadeias de caracteres como DT_DATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET. Os valores de data/hora em formatos truncados são convertidos. A tabela a seguir lista os valores que são adicionados nas partes de data e hora ausentes.  
  
|Parte de data e hora|Preenchimento|  
|---------------------|-------------|  
|Seconds (segundos)|Adicione 00.|  
|Minutes (minutos)|Adicionar 00:00.|  
|Hora|Adicione 00:00:00.|  
|Day|Adicione 01 para o dia do mês.|  
|Month|Adicione 01 para o mês do ano.|  
  
 Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
  
