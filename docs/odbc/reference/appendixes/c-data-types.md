---
title: C Tipos de Dados | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292296"
---
# <a name="c-data-types"></a>Tipos de dados do C
Os tipos de dados ODBC C indicam o tipo de dados de buffers C usados para armazenar dados no aplicativo.  
  
 Todos os drivers devem suportar todos os tipos de dados C. Isso é necessário porque todos os drivers devem suportar todos os tipos C aos quais os tipos de SQL que eles suportam podem ser convertidos, e todos os drivers suportam pelo menos um tipo de SQL de caracteres. Como o tipo SQL de caractere pode ser convertido para e de todos os tipos C, todos os drivers devem suportar todos os tipos C.  
  
 O tipo de dados C é especificado nas funções **SQLBindCol** e **SQLGetData** com o argumento *TargetType* e na função **SQLBindParameter** com o argumento *ValueType.* Ele também pode ser especificado ligando para **SQLSetDescField** para definir o campo SQL_DESC_CONCISE_TYPE de um ARD ou APD, ou ligando para **SQLSetDescRec** com o argumento *Tipo* (e o argumento *SubTipo,* se necessário) e o argumento *DescritorHandle* definido para a alça de um ARD ou APD.  
  
 As tabelas a seguir listam identificadores de tipo válidos para os tipos de dados C. A tabela também lista o tipo de dados ODBC C que corresponde a cada identificador e a definição desse tipo de dados.  
  
|Identificador de tipo C|Tipo ODBC C|Tipo de C|  
|-----------------------|--------------------|------------|  
|SQL_C_CHAR|SQLCHAR *|unsigned char *|  
|SQL_C_WCHAR|SQLWCHAR *|wchar_t *|  
|SQL_C_SSHORT[j]|SQLSMALLINT|short int|  
|SQL_C_USHORT[j]|SQLUSMALLINT|unsigned short int|  
|SQL_C_SLONG[j]|SQLINTEGER|long int|  
|SQL_C_ULONG[j]|SQLUINTEGER|unsigned long int|  
|SQL_C_FLOAT|SQLREAL|FLOAT|  
|SQL_C_DOUBLE|SQLDOUBLE, SQLFLOAT|double|  
|SQL_C_BIT|SQLCHAR|unsigned char|  
|SQL_C_STINYINT[j]|SQLSCHAR|signed char|  
|SQL_C_UTINYINT[j]|SQLCHAR|unsigned char|  
|SQL_C_SBIGINT|SQLBIGINT|_int64[h]|  
|SQL_C_UBIGINT|SQLUBIGINT|_int64 não assinado[h]|  
|SQL_C_BINARY|SQLCHAR *|unsigned char *|  
|SQL_C_BOOKMARK[i]|Indicador|int longo não assinado[d]|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|  
|Todos os tipos de dados do intervalo C|SQL_INTERVAL_STRUCT|Consulte a seção [Estrutura do Intervalo C,](../../../odbc/reference/appendixes/c-interval-structure.md) mais tarde neste apêndice.|  
  
 **Identificador de tipo C** SQL_C_TYPE_DATE[c]  
  
 **Tipo ODBC C** SQL_DATE_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagDATE_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;    
} DATE_STRUCT;[a]  
```  
  
 **Identificador de tipo C** SQL_C_TYPE_TIME[c]  
  
 **Tipo ODBC C** SQL_TIME_STRUCT  
  
 **Tipo de C**  
  
```  
struct tagTIME_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
} TIME_STRUCT;[a]  
```  
  
 **Identificador de tipo C** SQL_C_TYPE_TIMESTAMP[c]  
  
 **Tipo ODBC C** SQL_TIMESTAMP_STRUCT  
  
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
  
 **Tipo ODBC C** SQL_NUMERIC_STRUCT  
  
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
  
 **Tipo ODBC C** Sqlguid  
  
 **Tipo de C**  
  
```  
struct tagSQLGUID {  
   DWORD Data1;  
   WORD Data2;  
   WORD Data3;  
   BYTE Data4[8];  
} SQLGUID;[k]  
```  
  
 [a] Os valores dos campos do ano, mês, dia, hora, minuto e segundo nos tipos de dados de data C devem estar em conformidade com as restrições do calendário gregoriano. (Veja [as restrições do calendário gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md) mais tarde neste apêndice.)  
  
 [b] O valor do campo de fração é o número de bilionésimos de segundo e varia de 0 a 999.999.999 (1 menos de 1 bilhão). Por exemplo, o valor do campo de fração por meio segundo é de 500.000.000, para um milésimo de segundo (um milissegundo) é de 1.000.000, para um milionésimo de segundo (um microssegundo) é de 1.000, e para um bilionésimo de segundo (um nanossegundo) é 1.  
  
 [c] Em ODBC 2. *x*, os tipos de dados de data, hora e carimbo de data C são SQL_C_DATE, SQL_C_TIME e SQL_C_TIMESTAMP.  
  
 [d] As aplicações ODBC 3 *.x* devem usar SQL_C_VARBOOKMARK, não SQL_C_BOOKMARK. Quando um aplicativo ODBC 3 *.x* funciona com um ODBC 2. *x* driver, o ODBC 3 *.x* Driver Manager irá mapear SQL_C_VARBOOKMARK para SQL_C_BOOKMARK.  
  
 [e] Um número é armazenado no campo *val* da estrutura SQL_NUMERIC_STRUCT como um inteiro escalado, em modo pouco endiano (sendo o byte mais à esquerda o byte menos significativo). Por exemplo, o número 10.001 base 10, com uma escala de 4, é dimensionado para um inteiro de 100010. Por se trata de 186AA em formato hexadecimal, o valor em SQL_NUMERIC_STRUCT seria "AA 86 01 00 00 ... 00", com o número de bytes definidos pelo SQL_MAX_NUMERIC_LEN **#define**.  
  
 Para obter mais informações sobre **SQL_NUMERIC_STRUCT,** consulte [HOWTO: Recuperando dados numéricos com SQL_NUMERIC_STRUCT](retrieve-numeric-data-sql-numeric-struct-kb222831.md).  
  
 [f] Os campos de precisão e escala do SQL_C_NUMERIC tipo de dados são usados para entrada de um aplicativo e para saída do driver para o aplicativo. Quando o driver grava um valor numérico no SQL_NUMERIC_STRUCT, ele usará seu próprio padrão específico para o driver como valor para o campo *de precisão,* e usará o valor no campo SQL_DESC_SCALE do descritor de aplicativo (que é padrão para 0) para o campo *de escala.* Um aplicativo pode fornecer seus próprios valores para precisão e escala, definindo os campos SQL_DESC_PRECISION e SQL_DESC_SCALE do descritor do aplicativo.  
  
 [g] O campo de sinais é 1 se positivo, 0 se negativo.  
  
 [h] _int64 pode não ser fornecido por alguns compiladores.  
  
 [i] _SQL_C_BOOKMARK foi preterida em ODBC 3 *.x*.  
  
 [j] _SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT foram substituídos na ODBC por tipos assinados e não assinados: SQL_C_SSHORT e SQL_C_USHORT, SQL_C_SLONG e SQL_C_ULONG, e SQL_C_STINYINT e SQL_C_UTINYINT. Um driver ODBC 3 *.x* que deve funcionar com ODBC 2. *x* aplicativos devem suportar SQL_C_SHORT, SQL_C_LONG e SQL_C_TINYINT, porque quando são chamados, o Driver Manager passa para o motorista.  
  
 [k] SQL_C_GUID pode ser convertido apenas para SQL_CHAR ou SQL_WCHAR.  
  
 Esta seção contém o seguinte tópico.  
  
-   [Estruturas de inteiro de 64 bits](../../../odbc/reference/appendixes/64-bit-integer-structures.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados do C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)
