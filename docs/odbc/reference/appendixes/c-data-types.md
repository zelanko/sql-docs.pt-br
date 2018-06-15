---
title: Tipos de dados C | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 288ca6cbd5553b963131d34b8e63640518f70ef4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912731"
---
# <a name="c-data-types"></a>Tipos de dados C
Tipos de dados ODBC C indicam o tipo de dados de C buffers usados para armazenar dados no aplicativo.  
  
 Todos os drivers devem dar suporte a todos os tipos de dados C. Isso é necessário porque todos os drivers devem dar suporte a todos os tipos de C para o qual os tipos SQL que dão suporte a eles podem ser convertidos e todos os drivers de suportam a pelo menos um caractere de tipo SQL. Porque o tipo de caractere SQL pode ser convertido para e de todos os tipos de C, todos os drivers devem dar suporte a todos os tipos C.  
  
 O tipo de dados C é especificado no **SQLBindCol** e **SQLGetData** funciona com o *TargetType* argumento e, no **SQLBindParameter**funcionar com o *ValueType* argumento. Ele também pode ser especificado ao chamar **SQLSetDescField** para definir o campo SQL_DESC_CONCISE_TYPE de descartar ou APD ou chamando **SQLSetDescRec** com o *tipo* argumento (e o *subtipo* argumento se necessário) e o *DescriptorHandle* argumento definido como o identificador de descartar ou APD.  
  
 As tabelas a seguir lista os identificadores de tipo válido para os tipos de dados C. A tabela também lista o tipo de dados ODBC C que corresponde a cada identificador e a definição deste tipo de dados.  
  
|Identificador de tipo C|Typedef ODBC C|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT [j]|SQLSMALLINT|short int|  
|SQL_C_USHORT [j]|SQLUSMALLINT|int curto não assinado|  
|SQL_C_SLONG [j]|SQLINTEGER|Long int|  
|SQL_C_ULONG [j]|SQLUINTEGER|int longo não assinado|  
|SQL_C_FLOAT|SQLREAL|float|  
|SQL_C_DOUBLE|SQLDOUBLE, SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|caracteres não assinados|  
|SQL_C_STINYINT [j]|SQLSCHAR|char assinada|  
|SQL_C_UTINYINT [j]|SQLCHAR|caracteres não assinados|  
|SQL_C_SBIGINT|SQLBIGINT|_int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|sem sinal _int64 [h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK [i]|INDICADOR|int longo não assinado [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|Todos os tipos de dados de intervalo de C|SQL_INTERVAL_STRUCT|Consulte o [C intervalo estrutura](../../../odbc/reference/appendixes/c-interval-structure.md) seção mais adiante neste apêndice.|  
  
 **O identificador de tipo C** SQL_C_TYPE_DATE [c]  
  
 **Typedef ODBC C** SQL_DATE_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **O identificador de tipo C** SQL_C_TYPE_TIME [c]  
  
 **Typedef ODBC C** SQL_TIME_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **O identificador de tipo C** SQL_C_TYPE_TIMESTAMP [c]  
  
 **Typedef ODBC C** SQL_TIMESTAMP_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagTIMESTAMP_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;[b]   
} TIMESTAMP_STRUCT;[a]  
```  
  
 **O identificador de tipo C** SQL_C_NUMERIC  
  
 **Typedef ODBC C** SQL_NUMERIC_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **O identificador de tipo C** SQL_C_GUID  
  
 **Typedef ODBC C** SQLGUID  
  
 **Tipo de C**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] os valores de ano, mês, dia, hora, minuto e segundo campos nos tipos de dados datetime C devem estar de acordo com as restrições do calendário gregoriano. (Consulte [restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) mais adiante neste apêndice.)  
  
 [b] o valor do campo de fração é o número de bilionésimos de segundo e varia de 0 a 999.999.999 (menos de 1 bilhão de 1). Por exemplo, o valor do campo de uma segunda metade da fração é 500,000,000, para um milésimos de segundo (de um milissegundo) é 1.000.000, para um milionésimo de segundo (um microssegundos) é 1.000 e para um bilionésimo de segundo (um nanossegundos) é 1.  
  
 [c] em ODBC 2. *x*, os tipos de dados C data, hora e carimbo de hora são SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP.  
  
 [d] ODBC 3 *. x* SQL_C_VARBOOKMARK, não SQL_C_BOOKMARK os aplicativos devem usar. Quando um ODBC 3 *. x* aplicativo funciona com um ODBC 2. *x* driver, o ODBC 3 *. x* Gerenciador de Driver será mapeada SQL_C_VARBOOKMARK SQL_C_BOOKMARK.  
  
 [e] um número é armazenado no *val* campo da estrutura SQL_NUMERIC_STRUCT como um inteiro de escala, no modo little endian (o byte mais à esquerda sendo o byte menos significativo). Por exemplo, o número 10.001 10 de base, com uma escala de 4, é dimensionado para um valor inteiro de 100010. Como isso é 186AA em formato hexadecimal, o valor em SQL_NUMERIC_STRUCT seria "AA 86 01 00 00... 00", com o número de bytes definida pelo SQL_MAX_NUMERIC_LEN **#define**.  
  
 Para obter mais informações sobre **SQL_NUMERIC_STRUCT**, consulte [como: recuperar dados numéricos com SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md).  
  
 [f], os campos de precisão e escala dos dados SQL_C_NUMERIC tipo areused para entrada de um aplicativo e de saída do driver para o aplicativo. Quando o driver grava um valor numérico para o SQL_NUMERIC_STRUCT, ele usará seu próprio padrão específicos de driver como o valor para o *precisão* campo e ele usará o valor do campo SQL_DESC_SCALE no (descritor de aplicativo qual padrão é 0) para o *escala* campo. Um aplicativo pode fornecer seus próprios valores para a precisão e escala, definindo os campos SQL_DESC_PRECISION e SQL_DESC_SCALE do descritor de aplicativo.  
  
 [g], o campo de entrada é 1 se for positivo, 0 se for negativo.  
  
 [h] _int64 não pode ser fornecido por alguns compiladores.  
  
 [i] _SQL_C_BOOKMARK foi preterido no ODBC 3 *. x*.  
  
 [j] _SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT foram substituídos no ODBC por tipos assinados e não assinados: SQL_C_SSHORT e SQL_C_USHORT, SQL_C_SLONG e SQL_C_ULONG e SQL_C_STINYINT e SQL_C_UTINYINT. Um ODBC 3 *. x* driver deve funcionar com ODBC 2. *x* aplicativos devem oferecer suporte a SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT, porque quando eles são chamados, o Gerenciador de Driver passa-los por meio do driver.  
  
 [k] SQL_C_GUID podem ser convertidos somente a SQL_CHAR ou SQL_WCHAR.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Estruturas de inteiro de 64 bits](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de dados do C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
