---
title: Mapeamento de SQLInstallTranslator | Microsoft Docs
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
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00fcaf15458873da56d1d37d2234fd14bf7bbbd0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlinstalltranslator-mapping"></a>Mapeamento de SQLInstallTranslator
Quando um ODBC 2. *x* aplicativo chama **SQLInstallTranslator** por meio de um ODBC 3 *. x* driver, o Gerenciador de Driver mapeia a chamada para **SQLInstallTranslatorEx**. Um aplicativo não deve chamar **SQLInstallTranslator** em ODBC 3 *. x* Gerenciador de Driver com o *lpszInfFile* argumento definido como um valor diferente de NULL. O ODBC. Arquivo INF usado no ODBC 2. *x* não é suportada em ODBC 3 *. x*, mesmo para compatibilidade com versões anteriores.
