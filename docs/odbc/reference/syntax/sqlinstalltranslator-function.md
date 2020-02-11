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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076112"
---
# <a name="sqlinstalltranslator-function"></a>Função SQLInstallTranslator
**Conformidade**  
 Versão introduzida: ODBC 2,5, preterido  
  
 **Resumo**  
 No ODBC 3,0, o **SQLInstallTranslator** foi substituído por [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md). As chamadas para **SQLInstallTranslator** serão mapeadas para **SQLInstallTranslatorEx**. Para obter mais informações, consulte **SQLInstallTranslatorEx**.  
  
 **SQLInstallTranslator** retornará false se um aplicativo o chamar no Gerenciador de driver ODBC *3. x* com o argumento *lpszInfFile* definido como um valor diferente de NULL. Não há mais suporte para o arquivo ODBC. inf usado no ODBC *2. x* no ODBC *3. x*, mesmo para compatibilidade com versões anteriores.
