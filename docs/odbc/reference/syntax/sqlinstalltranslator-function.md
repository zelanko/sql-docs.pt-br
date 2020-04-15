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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b094aa730fff6db80b9addb63a92bee0f5f85b2a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300316"
---
# <a name="sqlinstalltranslator-function"></a>Função SQLInstallTranslator
**Conformidade**  
 Versão introduzida: ODBC 2.5, Depreciada  
  
 **Resumo**  
 No ODBC 3.0, **o SQLInstallTranslator** foi substituído pelo [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). As chamadas para **SQLInstallTranslator** serão mapeadas para **SQLInstallTranslatorEx**. Para obter mais informações, consulte **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** retornará FALSO se um aplicativo o chamar no Gerenciador de Driver ODBC *3.x* com o argumento *lpszInfFile* definido como um valor diferente de NULL. O arquivo Odbc.inf usado no ODBC *2.x* não é mais suportado no ODBC *3.x*, mesmo para compatibilidade retrógrada.
