---
title: Mapeamento de SQLInstallTranslator | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cb17f3d77b39c43d1f20c4598ac0192332a9cf13
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlinstalltranslator-mapping"></a>Mapeamento de SQLInstallTranslator
Quando um ODBC 2. *x* aplicativo chama **SQLInstallTranslator** por meio de um ODBC 3*. x* driver, o Gerenciador de Driver mapeia a chamada para **SQLInstallTranslatorEx**. Um aplicativo não deve chamar **SQLInstallTranslator** em ODBC 3*. x* Gerenciador de Driver com o *lpszInfFile* argumento definido como um valor diferente de NULL. O ODBC. Arquivo INF usado no ODBC 2. *x* não é suportada em ODBC 3*. x*, mesmo para compatibilidade com versões anteriores.
