---
title: Função SQLInstallTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36e1c76e85aec665e8b9554a305ccef0444d27f3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlinstalltranslator-function"></a>Função SQLInstallTranslator
**Conformidade**  
 Versão introduzidas: ODBC 2.5, preterido  
  
 **Resumo**  
 No ODBC 3.0, **SQLInstallTranslator** foi substituído pelo [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Chamadas para **SQLInstallTranslator** serão mapeados para **SQLInstallTranslatorEx**. Para obter mais informações, consulte **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** retornará FALSE se um aplicativo chama em ODBC 3 *. x* Gerenciador de Driver com o *lpszInfFile* argumento definido como um valor diferente de NULL. O arquivo de Odbc.inf usado no ODBC 2. *x* não é suportada em ODBC 3 *. x*, mesmo para compatibilidade com versões anteriores.
