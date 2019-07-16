---
title: Mapeamento SQLInstallTranslator | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6433df796c88abd7873915266d1a2ca4041a5c62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125733"
---
# <a name="sqlinstalltranslator-mapping"></a>Mapeamento SQLInstallTranslator
Quando um ODBC *2.x* aplicativo chamará **SQLInstallTranslator** por meio de ODBC *3.x* driver, o Gerenciador de Driver mapeia a chamada para  **SQLInstallTranslatorEx**. Um aplicativo não deve chamar **SQLInstallTranslator** no ODBC *3.x* Gerenciador de Driver com o *lpszInfFile* argumento definido como um valor diferente de NULL. O ODBC. Arquivo INF usado no ODBC *2.x* não é mais suportada no ODBC *3.x*, mesmo para compatibilidade com versões anteriores.
