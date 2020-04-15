---
title: Argumentos de função Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a25dd6fe0a77aad5c5ec9ba15eaf12bd2ec3fc18
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284286"
---
# <a name="unicode-function-arguments"></a>Argumentos da função Unicode
O Gerenciador de driver ODBC 3.5 (ou superior) suporta versões ANSI e Unicode de todas as funções que aceitam ponteiros para strings de caracteres ou SQLPOINTER em seus argumentos. As funções Unicode são implementadas como funções (com um sufixo de *W),* não como macros. As funções ANSI (que podem ser chamadas com ou sem um sufixo de *A*) são idênticas às funções atuais da API ODBC.  
  
## <a name="remarks"></a>Comentários  
 Funções unicode que sempre retornam ou tomam strings ou argumentos de comprimento são passadas como contagem de caracteres. Para funções que retornam informações de comprimento para dados do servidor, o tamanho e a precisão do display são descritos em número de caracteres. Quando um comprimento (tamanho de transferência dos dados) pode se referir a dados de seqüência ou não, o comprimento é descrito em comprimentos de octeto. Por exemplo, **o SQLGetInfoW** ainda terá o comprimento como contagem de bytes, mas **o SQLExecDirectW** usará contagem de caracteres.  
  
 Contagem de caracteres refere-se ao número de bytes (octetos) para funções ANSI e ao número de WCHAR (palavras de 16 bits) para funções UNICODE. Em particular, uma seqüência de caracteres de byte duplo (DBCS) ou uma seqüência de caracteres multibytes (MBCS) pode ser composta de vários bytes. Uma seqüência de caracteres Unicode UTF-16 pode ser composta de vários WCHARs.  
  
 A seguir está uma lista das funções da API ODBC que suportam as versões Unicode (W) e ANSI (A):  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColAttributea**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
|**SQLColumns**|**SQlnativesqL**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**Sqlerror**|**Sqlsetconnectoption**|  
|**SQLExecDirect**|**Sqlsetcursorname**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**Opção SQLGetConnect**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
|**SQLGetDiagField**||  
  
 A seguir está uma lista das funções ODBC Installer e ODBC Translator que suportam as versões Unicode (W) e ANSI (A):  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**SQLInstallerError**|  
|**SQLDataSourceToDriver**|**Sqlinstallodbc**|  
|**SQLDriverToDataFonte**|**SQlReadfiledsn**|  
|**SQLGetAvailableDrivers**|**SQLremovedsnfromINI**|  
|**SQLGetDrivers instalados**|**SQLvaliddSN**|  
|**SqlGetTranslator**|**SQLWritedsntoINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]
>  As funções depreciadas têm suporte a mapeamento Unicode-to-ANSI porque o ODBC *3.x* Driver Manager suporta a recompilação de aplicativos ODBC *2.x* com o **#define**UNICODE .  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Aplicativos Unicode](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Drivers Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Mapeamento de função no Gerenciador de Driver](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
