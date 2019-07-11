---
title: SQLInstallTranslator Mapping | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 50bfa00f482110d3d0695ef249e8758b5db02c80
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792805"
---
# <a name="sqlinstalltranslator-mapping"></a>Mapeamento SQLInstallTranslator
Quando um ODBC *2.x* aplicativo chamará **SQLInstallTranslator** por meio de ODBC *3.x* driver, o Gerenciador de Driver mapeia a chamada para  **SQLInstallTranslatorEx**. Um aplicativo não deve chamar **SQLInstallTranslator** no ODBC *3.x* Gerenciador de Driver com o *lpszInfFile* argumento definido como um valor diferente de NULL. O ODBC. Arquivo INF usado no ODBC *2.x* não é mais suportada no ODBC *3.x*, mesmo para compatibilidade com versões anteriores.
