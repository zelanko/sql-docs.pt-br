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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68bb4daa47cb58d5a0ff7b680a2d2154fb14b345
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284309"
---
# <a name="interval-data-type-length"></a>Comprimento do tipo de dados de intervalo
As seguintes regras são usadas para determinar o comprimento de um tipo de dados de intervalo nos caracteres. O comprimento é expresso em número de caracteres. O número de bytes depende do conjunto de caracteres. O comprimento inclui os seguintes valores adicionados:  
  
-   Dois caracteres para cada campo no intervalo que não é o campo principal.  
  
-   Para o campo principal, o número de caracteres que é a precisão de liderança expressa ou implícita. Se a precisão principal não for especificada, o valor padrão será 2.  
  
-   Um personagem para o separador entre os campos.  
  
-   Um mais a precisão expressa ou implícita segundos. Se a precisão de segundos não for especificada, o valor padrão será 6.  
  
 Os valores específicos do comprimento da coluna para cada tipo de dados de intervalo estão contidos no [Tamanho da coluna](../../../odbc/reference/appendixes/column-size.md).
