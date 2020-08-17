---
description: Tipos de dados com suporte
title: Tipos de dados com suporte | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349636553112449485d99fed269a43069974fccf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88385822"
---
# <a name="supported-data-types"></a>Tipos de dados com suporte
Os tipos de dados com suporte de DBMSs variam consideravelmente. Um aplicativo pode determinar os nomes e as características dos tipos de dados com suporte chamando **SQLGetTypeInfo**. Devido à grande variação em nomes de tipos de dados, o aplicativo deve usar os nomes de tipo de dados retornados por **SQLGetTypeInfo** em instruções **CREATE TABLE** . Para obter mais informações, consulte [tipos de dados em ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
