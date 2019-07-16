---
title: Função SQLInstallTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5b973332c2fe0fa541635d326a3a5adecf6ae91
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076112"
---
# <a name="sqlinstalltranslator-function"></a>Função SQLInstallTranslator
**Conformidade com**  
 Versão introduzida: ODBC 2.5, preterido  
  
 **Resumo**  
 No ODBC 3.0 **SQLInstallTranslator** foi substituído pelo [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Chamadas para **SQLInstallTranslator** serão mapeados para **SQLInstallTranslatorEx**. Para obter mais informações, consulte **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** retornará FALSE se um aplicativo chama no ODBC *3.x* Gerenciador de Driver com o *lpszInfFile* argumento definido como um valor diferente de NULL. O arquivo de Odbc.inf usado no ODBC *2.x* não é mais suportada no ODBC *3.x*, mesmo para compatibilidade com versões anteriores.
