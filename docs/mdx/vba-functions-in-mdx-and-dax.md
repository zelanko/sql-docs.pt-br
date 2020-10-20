---
description: Funções VBA no MDX e no DAX
title: Funções VBA em MDX e DAX | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0dcbf0f0321ddc0c1959c4681c0b1dddf49c1aba
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192286"
---
# <a name="vba-functions-in-mdx-and-dax"></a>Funções VBA no MDX e no DAX


  Este documento contém uma referência cruzada de todas as funções do VBA disponíveis em [Visual Basic for Applications funções](/office/vba/Language/Reference/functions-visual-basic-for-applications) com suporte no MDX; Além disso, a lista inclui uma observação quando há equivalência funcional com a linguagem DAX.  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Referência a funções do Visual Basic for Applications  
  
|Nome da função|Com suporte|Observações|  
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
|Data|Somente MDX|**Aviso** O DAX implementa uma função diferente com o mesmo nome; a função data (ano, mês, dia), usada para gerar um valor de tipo de data dos argumentos especificados|  
|DateAdd|Somente MDX|**Aviso** O DAX implementa uma função diferente com o mesmo nome; a função DATEADD ( \<dates> , <number_of_intervals> \<interval> ), usada para deslocar as datas determinadas por um número de intervalos determinados|  
|DateDiff|Somente MDX||  
|DatePart|Somente MDX||  
|DateSerial|Somente MDX||  
|DateValue|DAX, MDX||  
|Dia|DAX, MDX||  
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
|Filtrar|Sem suporte|**Aviso** A linguagem MDX implementa uma função diferente com o mesmo nome; a função FILTER (Set_Expression, Logical_Expression) retorna o conjunto que resulta da filtragem de um conjunto especificado com base em um critério de pesquisa dos argumentos especificados<br /><br /> **Aviso** O DAX implementa uma função diferente com o mesmo nome; a função FILTER ( \<table> , \<filter> ) retorna uma tabela que representa um subconjunto de outra tabela ou expressão dos argumentos especificados|  
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
|Iif|Somente MDX|**Aviso** O DAX implementa uma função semelhante com a função Name: IF (logical_test, value_if_true, value_if_false).|  
|IMEStatus|Sem suporte||  
|Entrada|Sem suporte||  
|InputBox|Sem suporte||  
|InStr|Somente MDX||  
|InStrRev|Sem suporte||  
|Int|DAX, MDX||  
|IPmt|Somente MDX||  
|IRR|Somente MDX||  
|IsArray|Somente MDX||  
|Somente IsDateMDX||  
|IsEmpty|Somente MDX||  
|IsError|DAX, MDX||  
|IsMissing|Somente MDX||  
|IsNull|Somente MDX||  
|IsNumeric|Somente MDX||  
|IsObject|Sem suporte||  
|Join|Sem suporte||  
|LBound|Sem suporte||  
|LCase|Somente MDX||  
|Esquerda|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|Sem suporte||  
|LOF|Sem suporte||  
|Log|Somente MDX|**Importante** O DAX implementa uma função diferente com o mesmo nome; a função de LOG (número, base). Retorna o logaritmo de um número à base especificada dos argumentos determinados.|  
|LTrim|Somente MDX||  
|MacID|Sem suporte||  
|MacScript|Sem suporte||  
|Mid|DAX, MDX||  
|Minuto|DAX, MDX||  
|MIRR|Somente MDX||  
|Mês|DAX, MDX||  
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
|Tarifa|Somente MDX||  
|Substitua|Sem suporte||  
|RGB|Somente MDX||  
|Direita|DAX, MDX||  
|Rnd|Somente MDX||  
|Round|DAX, MDX||  
|RTrim|Somente MDX||  
|Segundo|DAX, MDX||  
|Seek|Sem suporte||  
|Sgn|DAX, MDX||  
|Shell|Sem suporte||  
|Sin|Somente MDX||  
|SLN|Somente MDX||  
|Space|Somente MDX||  
|Spc|Sem suporte||  
|Divisão|Sem suporte||  
|Sqr|Somente MDX||  
|Str|Somente MDX||  
|StrComp|Somente MDX||  
|StrConv|Somente MDX||  
|String|Somente MDX||  
|StrReverse|Sem suporte||  
|Alternar|Somente MDX||  
|SYD|Somente MDX||  
|Tab|Sem suporte||  
|Tan|Somente MDX||  
|Hora|Sem suporte||  
|Temporizador|Somente MDX||  
|TimeSerial|Somente MDX||  
|TimeValue|DAX, MDX||  
|Trim|DAX, MDX||  
|TypeName|Somente MDX||  
|UBound|Sem suporte||  
|UCase|Somente MDX||  
|Val|Somente MDX||  
|VarType|Sem suporte||  
|Weekday|DAX, MDX||  
|WeekdayName|Sem suporte||  
|Year|DAX, MDX||  
  
