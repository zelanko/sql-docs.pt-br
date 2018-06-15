---
title: Argumentos de função Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], functions
- functions [ODBC], Unicode functions
ms.assetid: eafe8c7e-f6d2-44d7-99ee-cf2148a30f4f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab660a9af95d6232f22c98a868da8fed9ebb0cae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917951"
---
# <a name="unicode-function-arguments"></a>Argumentos de função Unicode
O Gerenciador de Driver ODBC 3.5 (ou superior) oferece suporte a versões ANSI e Unicode de todas as funções que aceitam ponteiros para cadeias de caracteres ou SQLPOINTER em seus argumentos. As funções de Unicode são implementadas como funções (com um sufixo de *W*), e não como macros. As funções ANSI (que pode ser chamado com ou sem um sufixo de *um*) são idênticas às funções de API ODBC atuais.  
  
## <a name="remarks"></a>Remarks  
 Funções de Unicode que sempre retornaram ou colocar cadeias de caracteres ou argumentos de comprimento são passadas como contagem de caracteres. Para funções que retornam informações de comprimento de dados do servidor, o tamanho de exibição e a precisão são descritos em número de caracteres. Quando um comprimento (tamanho de transferência de dados) pode se referir aos dados de cadeia de caracteres ou não-String, o comprimento é descrito em comprimentos de octeto. Por exemplo, **SQLGetInfoW** ainda terão comprimento como contagem de bytes, mas **SQLExecDirectW** usará a contagem de caracteres.  
  
 Contagem de caracteres se refere ao número de bytes (octetos) para funções ANSI e o número de WCHAR (palavras de 16 bits) para funções UNICODE. Em particular, uma sequência de caracteres de dois bytes (DBCS) ou uma sequência de caracteres multibyte (MBCS) pode ser composta de vários bytes. Uma sequência de caracteres Unicode UTF-16 pode ser composta de vários WCHARs.  
  
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
  
 A seguir está uma lista de funções de instalador ODBC e conversor ODBC que dão suporte a versões Unicode (W) e ANSI (A):  
  
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
>  Preterido funções têm suporte de mapeamento de Unicode para ANSI porque o ODBC 3 *. x* Gerenciador de Driver dá suporte a recompilação ODBC 2. *x* aplicativos com o UNICODE **#define**.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Aplicativos Unicode](../../../odbc/reference/develop-app/unicode-applications.md)  
  
-   [Drivers Unicode](../../../odbc/reference/develop-app/unicode-drivers.md)  
  
-   [Mapeamento de função no Gerenciador de Driver](../../../odbc/reference/develop-app/function-mapping-in-the-driver-manager.md)
