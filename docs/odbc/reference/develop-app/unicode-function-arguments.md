---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3caa5feb387a7acdfa682f048bf77f2d999b560
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305785"
---
# <a name="unicode-function-arguments"></a>Argumentos da função Unicode
O Gerenciador de Driver ODBC 3.5 (ou superior) dá suporte a versões ANSI e Unicode de todas as funções que aceitam ponteiros para cadeias de caracteres ou SQLPOINTER em seus argumentos. As funções do Unicode são implementadas como funções (com um sufixo *W*), e não como macros. As funções ANSI (que pode ser chamado com ou sem um sufixo *um*) são idênticas as funções API ODBC atuais.  
  
## <a name="remarks"></a>Comentários  
 Funções de Unicode que sempre retornam ou levam cadeias de caracteres ou argumentos de comprimento são passadas como contagem de caracteres. Para funções que retornam informações de comprimento de dados do servidor, o tamanho de exibição e a precisão são descritas no número de caracteres. Quando um comprimento (tamanho da transferência de dados) pode se referir aos dados de cadeia de caracteres ou não cadeia de caracteres, o comprimento é descrito em comprimentos de octeto. Por exemplo, **SQLGetInfoW** ainda terão o comprimento como contagem de bytes, mas **SQLExecDirectW** usará a contagem de caracteres.  
  
 Contagem de caracteres refere-se para o número de bytes (octetos) para funções ANSI e o número de WCHAR (palavras de 16 bits) para funções UNICODE. Em particular, uma sequência de caracteres de byte duplo (DBCS) ou uma sequência de caracteres multibyte (MBCS) pode ser composta de vários bytes. Uma sequência de caracteres Unicode UTF-16 pode ser composta de vários WCHARs.  
  
 A seguir está uma lista das funções API ODBC que dão suporte a versões Unicode (W) e ANSI (A):  
  
|||  
|-|-|  
|**SQLBrowseConnect**|**SQLGetDiagField**|  
|**SQLColAttribute**|**SQLGetDiagRec**|  
|**SQLColAttributes**|**SQLGetInfo**|  
|**SQLColumnPrivileges**|**SQLGetStmtAttr**|  
|**SQLColumns**|**SQLNativeSQL**|  
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
  
 A seguir está uma lista das funções ODBC instalador e conversor ODBC que dão suporte a versões Unicode (W) e ANSI (A):  
  
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
>  Funções preteridas tem suporte de mapeamento de Unicode para ANSI porque o ODBC 3 *. x* Gerenciador de Driver dá suporte a recompilação do ODBC 2. *x* aplicativos com o UNICODE **#define**.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Aplicativos Unicode](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Drivers Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Mapeamento de função no Gerenciador de Driver](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
