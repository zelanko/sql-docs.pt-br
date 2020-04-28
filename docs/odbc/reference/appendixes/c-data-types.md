---
title: Tipos de dados C | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], C data types
- C data types [ODBC], about C data types
- C data types [ODBC]
- C buffers [ODBC]
ms.assetid: b681d260-3dbb-47df-a616-4910d727add7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 979bfe85e1e78b55718e1f12fdcfcc7583097bb4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292296"
---
# <a name="c-data-types"></a>Tipos de dados do C
Tipos de dados ODBC C indicam o tipo de dados dos buffers C usados para armazenar dados no aplicativo.  
  
 Todos os drivers devem oferecer suporte a todos os tipos de dados C. Isso é necessário porque todos os drivers devem dar suporte a todos os tipos de C aos quais os tipos SQL para os quais eles dão suporte podem ser convertidos e todos os drivers dão suporte a pelo menos um tipo de caractere SQL. Como o tipo de caractere SQL pode ser convertido em e de todos os tipos de C, todos os drivers devem dar suporte a todos os tipos de C.  
  
 O tipo de dados C é especificado nas funções **SQLBindCol** e **SQLGetData** com o argumento *TargetType* e na função **SQLBindParameter** com o argumento *ValueType* . Ele também pode ser especificado chamando **SQLSetDescField** para definir o campo de SQL_DESC_CONCISE_TYPE de um ARD ou APD, ou chamando **SQLSetDescRec** com o argumento de *tipo* (e o argumento de *subtipo* , se necessário) e o argumento *DESCRIPTORHANDLE* definido como o identificador de um ARD ou APD.  
  
 As tabelas a seguir listam identificadores de tipo válidos para os tipos de dados C. A tabela também lista o tipo de dados ODBC C que corresponde a cada identificador e a definição desse tipo de dados.  
  
|Identificador de tipo C|Typedef C ODBC|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR|wchar_t *|  
|SQL_C_SSHORT [j]|SQLSMALLINT|short int|  
|SQL_C_USHORT [j]|SQLUSMALLINT|unsigned short int|  
|SQL_C_SLONG [j]|SQLINTEGER|long int|  
|SQL_C_ULONG [j]|SQLUINTEGER|unsigned long int|  
|SQL_C_FLOAT|Sqlreal|FLOAT|  
|SQL_C_DOUBLE|sqlfloat|double|  
|SQL_C_BIT|SQLCHAR|unsigned char|  
|SQL_C_STINYINT [j]|SQLSCHAR|signed char|  
|SQL_C_UTINYINT [j]|SQLCHAR|unsigned char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64 [h]|  
|SQL_C_UBIGINT|SQLUBIGINT|_int64 não assinado [h]|  
|SQL_C_BINARY|SQLCHAR|unsigned char *|  
|SQL_C_BOOKMARK [i]|Indicador|int longo sem sinal [d]|  
|SQL_C_VARBOOKMARK|SQLCHAR|unsigned char *|  
|Todos os tipos de dados de intervalo de C|SQL_INTERVAL_STRUCT|Consulte a seção [estrutura do intervalo C](../../../odbc/reference/appendixes/c-interval-structure.md) , mais adiante neste apêndice.|  
  
 **Identificador de tipo C** SQL_C_TYPE_DATE [C]  
  
 **Typedef C ODBC** SQL_DATE_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **Identificador de tipo C** SQL_C_TYPE_TIME [C]  
  
 **Typedef C ODBC** SQL_TIME_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **Identificador de tipo C** SQL_C_TYPE_TIMESTAMP [C]  
  
 **Typedef C ODBC** SQL_TIMESTAMP_STRUCT  
  
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
  
 **Identificador de tipo C** SQL_C_NUMERIC  
  
 **Typedef C ODBC** SQL_NUMERIC_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagSQL_NUMERIC_STRUCT {  
   SQLCHAR precision;  
   SQLSCHAR scale;  
   SQLCHAR sign[g];  
   SQLCHAR val[SQL_MAX_NUMERIC_LEN];[e], [f]   
} SQL_NUMERIC_STRUCT;  
```  
  
 **Identificador de tipo C** SQL_C_GUID  
  
 **Typedef C ODBC** SQLGUID  
  
 **Tipo de C**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] os valores dos campos ano, mês, dia, hora, minuto e segundo nos tipos de dados DateTime C devem estar em conformidade com as restrições do calendário gregoriano. (Consulte [restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) mais adiante neste apêndice.)  
  
 [b] o valor do campo fração é o número de billionths de um segundo e varia de 0 a 999.999.999 (1 menos de 1.000.000.000). Por exemplo, o valor do campo de fração para um semestre é 500 milhões, por um segundo (um milissegundo) é 1 milhão, para um milionésimo de um segundo (um microssegundo) é 1.000, e para uma billionth de um segundo (um nanossegundo) é 1.  
  
 [c] no ODBC 2. *x*, os tipos de dados C Date, time e timestamp são SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP.  
  
 [d] os aplicativos ODBC 3 *. x* devem usar SQL_C_VARBOOKMARK, não SQL_C_BOOKMARK. Quando um aplicativo ODBC 3 *. x* funciona com um ODBC 2. *x* Driver, o Gerenciador de driver ODBC 3 *. x* mapeará SQL_C_VARBOOKMARK para SQL_C_BOOKMARK.  
  
 [e] um número é armazenado no campo *Val* da estrutura de SQL_NUMERIC_STRUCT como um inteiro dimensionado, no modo de little endian (o byte mais à esquerda é o byte menos significativo). Por exemplo, o número 10, 1 base 10, com uma escala de 4, é dimensionado para um inteiro de 100010. Como isso é 186AA no formato hexadecimal, o valor em SQL_NUMERIC_STRUCT seria "AA 86 01 00 00... 00 ", com o número de bytes definidos pelo **#define**de SQL_MAX_NUMERIC_LEN.  
  
 Para obter mais informações sobre **SQL_NUMERIC_STRUCT**, consulte [HOWTO: Recuperando dados numéricos com SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md).  
  
 [f] os campos de precisão e escala do tipo de dados SQL_C_NUMERIC areused para entrada de um aplicativo e para saída do driver para o aplicativo. Quando o driver grava um valor numérico na SQL_NUMERIC_STRUCT, ele usará seu próprio padrão específico de driver como o valor do campo *precisão* e usará o valor no campo SQL_DESC_SCALE do descritor de aplicativo (que usa como padrão 0) para o campo de *escala* . Um aplicativo pode fornecer seus próprios valores para precisão e escala definindo os campos SQL_DESC_PRECISION e SQL_DESC_SCALE do descritor de aplicativo.  
  
 [g] o campo de sinal será 1 se positivo, 0 se negativo.  
  
 [h] _int64 pode não ser fornecida por alguns compiladores.  
  
 [i] _SQL_C_BOOKMARK foi preterida no ODBC 3 *. x*.  
  
 [j] _SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT foram substituídos em ODBC por tipos assinados e sem sinal: SQL_C_SSHORT e SQL_C_USHORT, SQL_C_SLONG e SQL_C_ULONG e SQL_C_STINYINT e SQL_C_UTINYINT. Um driver ODBC 3 *. x* que deve funcionar com ODBC 2. os aplicativos *x* devem dar suporte a SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT, porque quando são chamados, o Gerenciador de driver os passa para o driver.  
  
 [k] SQL_C_GUID só podem ser convertidas em SQL_CHAR ou SQL_WCHAR.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Estruturas de inteiro de 64 bits](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
