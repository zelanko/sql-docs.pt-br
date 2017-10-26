---
title: "Função SQLInstallTranslator | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2b7efa21691627c346b6d3798ade158e946071e6
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlinstalltranslator-function"></a>Função SQLInstallTranslator
**Conformidade**  
 Versão introduzidas: ODBC 2.5, preterido  
  
 **Resumo**  
 No ODBC 3.0, **SQLInstallTranslator** foi substituído pelo [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). Chamadas para **SQLInstallTranslator** serão mapeados para **SQLInstallTranslatorEx**. Para obter mais informações, consulte **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** retornará FALSE se um aplicativo chama em ODBC 3*. x* Gerenciador de Driver com o *lpszInfFile* argumento definido como um valor diferente de NULL. O arquivo de Odbc.inf usado no ODBC 2. *x* não é suportada em ODBC 3*. x*, mesmo para compatibilidade com versões anteriores.

