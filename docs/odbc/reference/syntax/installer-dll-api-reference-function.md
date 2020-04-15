---
title: Função de referência da API do instalador DLL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installer DLL [ODBC]
ms.assetid: 47fcadc3-f102-4989-9ee7-a1c65233142a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3502dfe6cdf54214041e3654d20e1b6dd2ff6f21
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298776"
---
# <a name="installer-dll-api-reference-function"></a>Função de referência de API de DLL do instalador
Esta seção descreve a sintaxe das funções na API do instalador DLL. A API DLL do instalador consiste em 20 funções. Três dessas funções, **SQLGetTranslator,** **SQLRemoveDSNFromIni**e **SQLWriteDSNToIni,** são chamadas apenas por DLLs de configuração. As outras funções são chamadas pelos programas de configuração e administração.  
  
 Cada função é rotulada com a versão do ODBC em que foi introduzida.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Função SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)  
  
-   [Função SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)  
  
-   [Função SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)  
  
-   [Função SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)  
  
-   [Função SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)  
  
-   [Função SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)  
  
-   [Função SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)  
  
-   [Função SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)  
  
-   [Função SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)  
  
-   [Função SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)  
  
-   [Função SQLInstallTranslator](../../../odbc/reference/syntax/sqlinstalltranslator-function.md)  
  
-   [Função SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)  
  
-   [Função SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)  
  
-   [Função SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)  
  
-   [Função SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)  
  
-   [Função SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)  
  
-   [Função SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)  
  
-   [Função SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)  
  
-   [Função SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)  
  
-   [Função SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)  
  
-   [Função SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)  
  
-   [Função SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)  
  
-   [Função SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)  
  
-   [Função SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)  
  
-   [Função SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)
