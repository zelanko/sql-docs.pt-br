---
title: Suporte ao tipo de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 820e48a17e397bc9046c8ca431677074e69b8cb2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905831"
---
# <a name="data-type-support"></a>Suporte do tipo de dados
Drivers ODBC devem oferecer suporte a pelo menos uma das SQL_CHAR e SQL_VARCHAR. Suporte para outros tipos de dados é determinado pelo nível de conformidade do driver ou fonte de dados SQL-92. Um aplicativo deve chamar **SQLGetTypeInfo** para determinar os tipos de dados com suporte pelo driver.  
  
 Para obter mais informações sobre tipos de dados, consulte [tipos de dados do apêndice d:](../../../odbc/reference/appendixes/appendix-d-data-types.md).
