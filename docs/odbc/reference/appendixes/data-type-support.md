---
description: Suporte do tipo de dados
title: Suporte ao tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ab0fd163713a7f6657d8ce446336f5c35a3dd00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456633"
---
# <a name="data-type-support"></a>Suporte do tipo de dados
Os drivers ODBC devem oferecer suporte a pelo menos um dos SQL_CHAR e SQL_VARCHAR. O suporte para outros tipos de dados é determinado pelo nível de conformidade do SQL-92 da fonte de dados ou do driver. Um aplicativo deve chamar **SQLGetTypeInfo** para determinar os tipos de dados com suporte pelo driver.  
  
 Para obter mais informações sobre tipos de dados, consulte o [Apêndice D: tipos de dados](../../../odbc/reference/appendixes/appendix-d-data-types.md).
