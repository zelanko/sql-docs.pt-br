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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1a0099e298b0326b5ccc19d6281fa3a091d57a2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282478"
---
# <a name="parameter-markers-in-procedure-calls"></a>Marcadores de parâmetro em chamadas de procedimento
Ao chamar procedimentos que aceitam parâmetros, aplicativos interoperáveis devem usar marcadores de parâmetro em vez de valores de parâmetro literais. Algumas fontes de dados não dão suporte ao uso de valores de parâmetro literais em chamadas de procedimento. Para obter mais informações sobre parâmetros, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md). Para obter mais informações sobre procedimentos de chamada, consulte [chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md), mais adiante nesta seção.
