---
title: Conversões de SQL para C | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC], SQL to C
ms.assetid: 059431e2-a65c-4587-ba4a-9929a1611e96
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 094a968fb48c9eabf554bfdccb89efc69e12391a
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427965"
---
# <a name="conversions-from-sql-to-c"></a>Conversões de SQL em C
  A seguinte tabela lista aspectos a serem considerados quando você converte tipos de data/hora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em tipos do C.  
  
## <a name="conversions"></a>Conversões  
  
||||||||||  
|-|-|-|-|-|-|-|-|-|  
||SQL_C_DATE|SQL_C_TIME|SQL_C_TIMESTAMP|SQL_C_SS_TIME2|SQL_C_SS_TIMESTAMPOFFSET|SQL_C_BINARY|SQL_C_CHAR|SQL_C_WCHAR|  
|SQL_CHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|1|1|1|  
|SQL_WCHAR|2,3,4,5|2,3,6,7,8|2,3,9,10,11|2,3,6,7|2,3,9,10,11|1|1|1|  
|SQL_TYPE_DATE|OK|12|13|12|13,23|14|16|16|  
|SQL_SS_TIME2|12|8|15|OK|10,23|17|16|16|  
|SQL_TYPE_TIMESTAMP|18|7,8|OK|7|23|19|16|16|  
|SQL_SS_TIMESTAMPOFFSET|18,22|7,8,20|20|7,20|OK|21|16|16|  
  
## <a name="key-to-symbols"></a>Legenda dos símbolos  
  
|Símbolo|Significado|  
|------------|-------------|  
|OK|Nenhum problema na conversão.|  
|1|Regras anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] se aplicam.|  
|2|Os espaços à esquerda e à direita são ignorados.|  
|3|A cadeia de caracteres é analisada em date, time, timezone ou timezoneoffset e permite até nove dígitos para segundos fracionários. Caso timezoneoffset seja analisado, a hora é convertida no fuso horário do cliente. Se ocorrer um erro durante essa conversão, um registro de diagnóstico é gerado com SQLSTATE 22018 e a mensagem "Estouro do campo Datetime".|  
|4|Caso o valor não seja date, timestamp ou timestampoffset válido, um registro de diagnóstico é gerado com SQLSTATE 22018 e a mensagem "Valor de caractere inválido para a especificação de difusão".|  
|5|Caso a hora seja diferente de zero, um registro de diagnóstico é gerado com SQLSTATE 01S07 e a mensagem "Truncamento fracionário".|  
|6|Caso o valor não seja time, timestamp ou timestampoffset válido, um registro de diagnóstico é gerado com SQLSTATE 22018 e a mensagem "Valor de caractere inválido para a especificação de difusão".|  
|7|O componente de data é ignorado.|  
|8|Caso os segundos fracionários sejam diferentes de zero, um registro de diagnóstico é gerado com SQLSTATE 01S07 e a mensagem "Truncamento fracionário".|  
|9|Caso o valor não seja date, time, timestamp ou timestampoffset válido, um registro de diagnóstico é gerado com SQLSTATE 22018 e a mensagem "Valor de caractere inválido para a especificação de difusão".|  
|10|Caso o valor não seja uma hora válida, o componente de data é definido como a data do cliente atual.|  
|11|Caso o valor seja uma data válida, a hora é definida como zero.|  
|12|Será gerado um registro de diagnóstico com SQLSTATE 07006 e a mensagem "Violação do atributo de tipo de dados restrito".|  
|13|A hora é definida como zero.|  
|14|Caso o buffer não seja grande o suficiente para acomodar SQL_DATE_STRUCT, um registro de diagnóstico é gerado com SQLSTATE 22003 e a mensagem "Valor numérico fora do intervalo".|  
|15|A data é definida como a data atual do cliente.|  
|16|Caso o buffer não seja grande o suficiente para acomodar o valor da cadeia de caracteres convertida, e sim apenas segundos fracionários, ocorre o truncamento, e um registro de diagnóstico é gerado com SQLSTATE 01004 e a mensagem "Dados de cadeia de caracteres truncados à direita". Caso o buffer não seja grande o suficiente para acomodar o valor da cadeia de caracteres sem truncamento dos componentes de data, hora ou deslocamento, um registro de diagnóstico é gerado com SQLSTATE 22003 e a mensagem "Valor numérico fora do intervalo". Observe que para date e timestampoffset, SQLSTATE 01004 não é possível porque a parte mais à direita da cadeia de caracteres convertida não contém segundos fracionários. Dessa forma, qualquer truncamento causa a perda de dados.|  
|17|Caso buffer não seja grande o suficiente para acomodar um SQL_SS_TIME2_STRUCT, um registro de diagnóstico é gerado com SQLSTATE 22003 e a mensagem "Valor numérico fora do intervalo".|  
|18|Caso a hora seja diferente de zero, um registro de diagnóstico é gerado com SQLSTATE 01S07 e a mensagem "Truncamento fracionário".|  
|19|Se o tipo de servidor for datetime ou smalldatetime, o valor corresponderá ao formato com fio TDS e será um valor de quatro bytes para smalldatetime e de oito para datetime.<br /><br /> Caso o tipo de servidor seja datetime2, o valor é retornado como SQL_TIMESTAMP_STRUCT. Caso o buffer não seja grande o suficiente para acomodar o valor retornado, um registro de diagnóstico é gerado com SQLSTATE 22003 e a mensagem "Valor numérico fora do intervalo".|  
|20|A hora é convertida para o fuso horário do cliente. Se ocorrer um erro durante esta conversão, um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Estouro do campo datetime".|  
|21|Caso o buffer seja grande o suficiente para acomodar um SQL_SS_TIMESTAMPOFFSET_STRUCT, o valor é retornado como SQL_SS_TIMESTAMPOFFSET_STRUCT. Caso contrário, um registro de diagnóstico é gerado com SQLSTATE 22003 e a mensagem "Valor numérico fora do intervalo".|  
|22|O valor é convertido no fuso horário do cliente antes da extração da data. Isso proporciona consistência em relação às demais conversões com tipos timestampoffset. Se ocorrer um erro durante esta conversão, um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Estouro do campo datetime". Isso pode resultar em uma data diferente do valor obtido pelo truncamento simples.|  
  
 A tabela neste tópico descreve conversões entre o tipo retornado para o cliente e o tipo na associação. Para parâmetros de saída, se o tipo de servidor especificado em SQLBindParameter não coincide com o tipo real no servidor, será executada uma conversão implícita pelo servidor e o tipo retornado para o cliente corresponderá ao tipo especificado por meio de SQLBindParameter. Isso pode levar a resultados de conversão inesperados quando as regras de conversão do servidor são diferentes das listadas na tabela anterior. Por exemplo, quando uma data padrão precisar ser fornecida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa 1900-1-1, e não a data atual.  
  
## <a name="see-also"></a>Consulte também  
 [Aprimoramentos de data e hora &#40;ODBC&#41;](date-and-time-improvements-odbc.md)  
  
  
