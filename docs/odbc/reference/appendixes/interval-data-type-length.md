---
title: Comprimento do tipo de dados de intervalo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16d0590d3297b52891bf399822ce984674022583
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188922"
---
# <a name="interval-data-type-length"></a>Comprimento do tipo de dados de intervalo
As regras a seguir são usadas para determinar o comprimento de um tipo de dados de intervalo em caracteres. Tamanho é expresso em número de caracteres. O número de bytes depende do conjunto de caracteres. O comprimento inclui os seguintes valores adicionados juntos:  
  
-   Dois caracteres para cada campo no intervalo de que não está no campo à esquerda.  
  
-   O campo à esquerda, o número de caracteres que é a precisão expressa ou implícita à esquerda. Se a precisão à esquerda não for especificada, o valor padrão é 2.  
  
-   Um caractere para o separador entre os campos.  
  
-   Um mais a precisão de segundos expressa ou implícita. Se a precisão de segundos não for especificada, o valor padrão é 6.  
  
 Os valores de comprimento de coluna específicos para cada tipo de dados de intervalo contidos no [tamanho da coluna](../../../odbc/reference/appendixes/column-size.md).
