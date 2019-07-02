---
title: As funções do VBA no MDX e DAX | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f6b6d89ced88a570ce242ae9490d4c6d8bd6ac8
ms.sourcegitcommit: 0b0f5aba602732834c8439c192d95921149ab4c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67500043"
---
# <a name="vba-functions-in-mdx-and-dax"></a>Funções VBA no MDX e no DAX


  Este documento contém uma referência cruzada de todas as funções VBA disponíveis em [Visual Basic para aplicativos de funções](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) que têm suporte no MDX; Além disso, a lista inclui uma nota quando há uma equivalência funcional com a linguagem DAX .  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Referência a funções do Visual Basic for Applications  
  
|Nome da função|Tem suporte|Observações|  
|-------------------|---------------|-----------|  
|Abs|DAX, MDX||  
|Array|Sem suporte||  
|Asc|Somente MDX||  
|AscW|Somente MDX||  
|Atn|Somente MDX||  
|CallByName|Sem suporte||  
|CBool|Somente MDX||  
|CByte|Somente MDX||  
|CCur|Somente MDX||  
|CDate|Somente MDX||  
|CDbl|Somente MDX||  
|CDec|Somente MDX||  
|Choose|Somente MDX||  
|Chr|Somente MDX||  
|CInt|Somente MDX||  
|CLng|Somente MDX||  
|CLngLng|Sem suporte||  
|CLngPtr|Sem suporte||  
|Comando|Sem suporte||  
|Cos|Somente MDX||  
|CreateObject|Sem suporte||  
|CSng|Somente MDX||  
|CStr|Somente MDX||  
|CurDir|Sem suporte||  
|CVar|Somente MDX||  
|CVErr|Sem suporte||  
|Date|Somente MDX|**Aviso** DAX implementa uma função diferente com o mesmo nome; a função Data (ano, mês, dia), usado para gerar um valor de tipo de data dos argumentos determinados|  
|DateAdd|Somente MDX|**Aviso** DAX implementa uma função diferente com o mesmo nome; a DATEADD (\<datas >, < number_of_intervals >\<intervalo >) função, usado para deslocar as datas determinadas por um número de intervalos determinados|  
|DateDiff|Somente MDX||  
|DatePart|Somente MDX||  
|DateSerial|Somente MDX||  
|DateValue|DAX, MDX||  
|Day|DAX, MDX||  
|DDB|Somente MDX||  
|Dir|Sem suporte||  
|DoEvents|Sem suporte||  
|Environ|Sem suporte||  
|EOF|Sem suporte||  
|Erro|Sem suporte||  
|Exp|DAX, MDX||  
|FileAttr|Sem suporte||  
|FileDateTime|Sem suporte||  
|FileLen|Sem suporte||  
|Filtrar|Sem suporte|**Aviso** MDX implementa uma função diferente com o mesmo nome; a função FILTER (Set_Expression, Logical_Expression) retorna o conjunto resultante da filtragem de um conjunto especificado com base em um critério de pesquisa dos argumentos determinados<br /><br /> **Aviso** DAX implementa uma função diferente com o mesmo nome; o filtro (\<tabela >,\<filtro >) função retorna uma tabela que representa um subconjunto de outra tabela ou expressão dos argumentos determinados|  
|Fix|Somente MDX||  
|Formato (Visual Basic for Applications)|DAX, MDX||  
|FormatCurrency|Sem suporte||  
|FormatDateTime|Sem suporte||  
|FormatNumber|Sem suporte||  
|FormatPercent|Sem suporte||  
|FreeFile|Sem suporte||  
|FV|Somente MDX||  
|GetAllSettings|Sem suporte||  
|GetAttr|Sem suporte||  
|GetObject|Sem suporte||  
|GetSetting|Sem suporte||  
|Hex|Somente MDX||  
|Hora|DAX, MDX||  
|Iif|Somente MDX|**Aviso** DAX implementa uma função semelhante com o nome: IF (logical_test, value_if_true, value_if_false) função.|  
|IMEStatus|Sem suporte||  
|Entrada|Sem suporte||  
|InputBox|Sem suporte||  
|InStr|Somente MDX||  
|InStrRev|Sem suporte||  
|Int|DAX, MDX||  
|IPmt|Somente MDX||  
|IRR|Somente MDX||  
|IsArray|Somente MDX||  
|IsDateMDX only||  
|IsEmpty|Somente MDX||  
|IsError|DAX, MDX||  
|IsMissing|Somente MDX||  
|IsNull|Somente MDX||  
|IsNumeric|Somente MDX||  
|IsObject|Sem suporte||  
|Join|Sem suporte||  
|LBound|Sem suporte||  
|LCase|Somente MDX||  
|Left (à esquerda)|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|Sem suporte||  
|LOF|Sem suporte||  
|Log|Somente MDX|**Importante** DAX implementa uma função diferente com o mesmo nome; a função LOG (número, base). Retorna o logaritmo de um número à base especificada dos argumentos determinados.|  
|LTrim|Somente MDX||  
|MacID|Sem suporte||  
|MacScript|Sem suporte||  
|Mid|DAX, MDX||  
|Minuto|DAX, MDX||  
|MIRR|Somente MDX||  
|Month|DAX, MDX||  
|MonthName|Sem suporte||  
|MsgBox|Sem suporte||  
|Agora|DAX, MDX||  
|NPer|Somente MDX||  
|NPV|Somente MDX||  
|Oct|Somente MDX||  
|Partition|Somente MDX||  
|Pmt|Somente MDX||  
|PPmt|Somente MDX||  
|PV|Somente MDX||  
|QBColor|Somente MDX||  
|Rate|Somente MDX||  
|Substituir|Sem suporte||  
|RGB|Somente MDX||  
|Right (à direita)|DAX, MDX||  
|Rnd|Somente MDX||  
|Arredondamento|DAX, MDX||  
|RTrim|Somente MDX||  
|Segundo|DAX, MDX||  
|Seek|Sem suporte||  
|Sgn|DAX, MDX||  
|Shell|Sem suporte||  
|Sin|Somente MDX||  
|SLN|Somente MDX||  
|Space|Somente MDX||  
|Spc|Sem suporte||  
|divisão|Sem suporte||  
|Sqr|Somente MDX||  
|Str|Somente MDX||  
|StrComp|Somente MDX||  
|StrConv|Somente MDX||  
|Cadeia de caracteres|Somente MDX||  
|StrReverse|Sem suporte||  
|Alternar|Somente MDX||  
|SYD|Somente MDX||  
|Tab|Sem suporte||  
|Tan|Somente MDX||  
|Time|Sem suporte||  
|Timer|Somente MDX||  
|TimeSerial|Somente MDX||  
|TimeValue|DAX, MDX||  
|Trim|DAX, MDX||  
|TypeName|Somente MDX||  
|UBound|Sem suporte||  
|UCase|Somente MDX||  
|Val|Somente MDX||  
|VarType|Sem suporte||  
|Dia de semana|DAX, MDX||  
|WeekdayName|Sem suporte||  
|Year|DAX, MDX||  
  
  
