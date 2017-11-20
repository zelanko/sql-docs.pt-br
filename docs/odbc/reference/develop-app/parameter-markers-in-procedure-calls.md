---
title: "Marcadores de parâmetro em chamadas de procedimento | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 206f9072242ba103bb39b01ead1393cc469a4700
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-markers-in-procedure-calls"></a>Marcadores de parâmetro em chamadas de procedimento
Ao chamar procedimentos que aceitam parâmetros, aplicativos interoperáveis devem usar marcadores de parâmetro em vez de valores de parâmetro literal. Algumas fontes de dados não suporta o uso de valores de parâmetro literal em chamadas de procedimento. Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md). Para obter mais informações sobre como chamar procedimentos, consulte [chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md), mais adiante nesta seção.

