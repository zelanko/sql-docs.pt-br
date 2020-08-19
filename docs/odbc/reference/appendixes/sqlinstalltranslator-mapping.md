---
description: Mapeamento SQLInstallTranslator
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc571e305070e4afba6dc7c647d18a6790c011f0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448965"
---
# <a name="sqlinstalltranslator-mapping"></a>Mapeamento SQLInstallTranslator
Quando um aplicativo ODBC *2. x* chama **SQLInstallTranslator** por meio de um driver ODBC *3. x* , o Gerenciador de driver mapeia a chamada para **SQLInstallTranslatorEx**. Um aplicativo não deve chamar **SQLInstallTranslator** no Gerenciador de driver do ODBC *3. x* com o argumento *lpszInfFile* definido com um valor diferente de NULL. O ODBC. Não há mais suporte para o arquivo INF usado no ODBC *2. x* no ODBC *3. x*, mesmo para compatibilidade com versões anteriores.
