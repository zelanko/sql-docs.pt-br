---
title: Marcadores de parâmetro em chamadas de procedimento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- parameter markers [ODBC]
- interoperability of SQL statements [ODBC], parameter markers
ms.assetid: cda56f2b-6eec-4cbc-8dbb-36d8fa9f9216
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3bb24fb628e9e49fd94104af05217511a8f57c3e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912312"
---
# <a name="parameter-markers-in-procedure-calls"></a>Marcadores de parâmetro em chamadas de procedimento
Ao chamar procedimentos que aceitam parâmetros, os aplicativos interoperáveis devem usar marcadores de parâmetro em vez de valores de parâmetro literal. Algumas fontes de dados não suportam o uso de valores de parâmetro literal em chamadas de procedimento. Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md). Para obter mais informações sobre como chamar procedimentos, consulte [chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md), mais adiante nesta seção.
