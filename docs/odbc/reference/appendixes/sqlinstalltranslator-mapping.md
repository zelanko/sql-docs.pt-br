---
title: Mapeamento de SQLInstallTranslator | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125733"
---
# <a name="sqlinstalltranslator-mapping"></a>Mapeamento SQLInstallTranslator
Quando um aplicativo ODBC *2. x* chama **SQLInstallTranslator** por meio de um driver ODBC *3. x* , o Gerenciador de driver mapeia a chamada para **SQLInstallTranslatorEx**. Um aplicativo não deve chamar **SQLInstallTranslator** no Gerenciador de driver do ODBC *3. x* com o argumento *lpszInfFile* definido com um valor diferente de NULL. O ODBC. Não há mais suporte para o arquivo INF usado no ODBC *2. x* no ODBC *3. x*, mesmo para compatibilidade com versões anteriores.
