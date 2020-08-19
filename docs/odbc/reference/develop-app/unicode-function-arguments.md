---
description: Argumentos da função Unicode
title: Argumentos da função Unicode | Microsoft Docs
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
ms.openlocfilehash: d2d59cad60855c670f7c7e2b189ad3c97a3027b9
ms.sourcegitcommit: 19ae05bc69edce1e3b3d621d7fdd45ea5f74969d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2020
ms.locfileid: "88564034"
---
# <a name="unicode-function-arguments"></a>Argumentos da função Unicode
O Gerenciador de driver ODBC 3,5 (ou superior) dá suporte a versões ANSI e Unicode de todas as funções que aceitam ponteiros para cadeias de caracteres ou sqlpointr em seus argumentos. As funções Unicode são implementadas como funções (com um sufixo de *W*), não como macros. As funções ANSI (que podem ser chamadas com ou sem um sufixo de *a*) são idênticas às funções da API ODBC atual.  
  
## <a name="remarks"></a>Comentários  
 Para funções Unicode que sempre retornam ou assumem cadeias de caracteres ou argumentos de comprimento, os argumentos são passados como contagem de caractere. Para funções que retornam informações de comprimento para dados do servidor, o tamanho de exibição e a precisão são descritos em número de caracteres. Quando um comprimento (tamanho de transferência dos dados) puder se referir a dados de cadeia de caracteres ou não de cadeia, o comprimento será descrito em comprimentos de octeto. Por exemplo, **SQLGetInfoW** ainda terá o comprimento como contagem de bytes, mas o **SQLExecDirectW** usará a contagem de caracteres.  
  
 A contagem de caracteres refere-se ao número de bytes (octetos) para funções ANSI e o número de WCHAR (palavras de 16 bits) para funções UNICODE. Em particular, uma seqüência de caracteres de byte duplo (DBCS) ou uma seqüência de caracteres multibyte (MBCS) pode ser composta por vários bytes. Uma sequência de caracteres Unicode UTF-16 pode ser composta por vários WCHARs.  
  
 Veja a seguir uma lista das funções da API ODBC que dão suporte às versões Unicode (W) e ANSI (A):  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagRec**|  
|**SQLColAttribute**|**SQLGetInfo**|  
|**SQLColAttributes**|**SQLGetStmtAttr**|  
|**SQLColumnPrivileges**|**SQLGetTypeInfo**|  
|**SQLColumns**|**SQLNativeSql**|  
|**SQLConnect**|**SQLPrepare**|  
|**SQLDataSources**|**SQLPrimaryKeys**|  
|**SQLDescribeCol**|**SQLProcedureColumns**|  
|**SQLDriverConnect**|**SQLProcedures**|  
|**SQLDrivers**|**SQLSetConnectAttr**|  
|**SQLError**|**SQLSetConnectOption**|  
|**SQLExecDirect**|**SQLSetCursorName**|  
|**SQLForeignKeys**|**SQLSetDescField**|  
|**SQLGetConnectAttr**|**SQLSetStmtAttr**|  
|**SQLGetConnectOption**|**SQLSpecialColumns**|  
|**SQLGetCursorName**|**SQLStatistics**|  
|**SQLGetDescField**|**SQLTablePrivileges**|  
|**SQLGetDescRec**|**SQLTables**|  
|**SQLGetDiagField**||  
  
 A seguir está uma lista de funções do ODBC Installer e do conversor ODBC que dão suporte às versões Unicode (W) e ANSI (A):  
  
|||  
|-|-|  
|**SQLConfigDataSource**|**SQLInstallDriverManager**|  
|**SQLCreateDataSource**|**SQLInstallerError**|  
|**SQLDataSourceToDriver**|**SQLInstallODBC**|  
|**SQLDriverToDataSource**|**SQLReadFileDSN**|  
|**SQLGetAvailableDrivers**|**SQLRemoveDSNFromINI**|  
|**SQLGetInstalledDrivers**|**SQLValidDSN**|  
|**SQLGetTranslator**|**SQLWriteDSNToINI**|  
|**SQLInstallDriver**||  
  
> [!NOTE]
>  Funções preteridas têm suporte para mapeamento de Unicode para ANSI porque o Gerenciador de driver ODBC *3. x* dá suporte à recompilação de aplicativos ODBC *2. x* com o **#define**Unicode.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Aplicativos Unicode](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Drivers Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Mapeamento de função no Gerenciador de Driver](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
