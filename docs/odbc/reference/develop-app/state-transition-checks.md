---
title: Verificações de transição de estado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], driver manager error checking
- state transition checks [ODBC]
- driver manager [ODBC], error checking
ms.assetid: 0706db7d-e125-4845-a13a-7fe4308f7360
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b337d317092ad6ae20cc91236d69c1314de96bce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107280"
---
# <a name="state-transition-checks"></a>Verificações de transição de estado
O Gerenciador de driver verifica se o estado do ambiente, da conexão ou da instrução é apropriado para a função que está sendo chamada. Por exemplo, uma conexão deve estar em um estado alocado quando **SQLConnect** for chamado; uma instrução deve estar em um estado preparado quando **SQLExecute** é chamado. O Gerenciador de driver retorna SQL_ERROR para erros de transição de estado.
