---
title: Marcadores de parâmetro em chamadas de procedimento | Microsoft Docs
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
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 744c9d8a7c75df66439794f1b461112800094ba7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-markers-in-procedure-calls"></a>Marcadores de parâmetro em chamadas de procedimento
Ao chamar procedimentos que aceitam parâmetros, aplicativos interoperáveis devem usar marcadores de parâmetro em vez de valores de parâmetro literal. Algumas fontes de dados não suporta o uso de valores de parâmetro literal em chamadas de procedimento. Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md). Para obter mais informações sobre como chamar procedimentos, consulte [chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md), mais adiante nesta seção.
