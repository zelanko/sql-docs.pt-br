---
title: Comprimento do tipo de dados de intervalo | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e642685b670fa872c1a34d2d10fed815e5a6fa7e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="interval-data-type-length"></a>Comprimento do tipo de dados de intervalo
As regras a seguir são usadas para determinar o comprimento de um tipo de dados de intervalo em caracteres. Comprimento é expresso em número de caracteres. O número de bytes depende do conjunto de caracteres. O comprimento inclui os seguintes valores adicionados juntos:  
  
-   Dois caracteres para cada campo no intervalo que não é o campo à esquerda.  
  
-   Para o campo principal, o número de caracteres que é a precisão à esquerda expressa ou implícita. Se a precisão à esquerda não for especificada, o valor padrão é 2.  
  
-   Um caractere para o separador entre os campos.  
  
-   Um mais a precisão de segundos explícita ou implícita. Se a precisão de segundos não for especificada, o valor padrão é 6.  
  
 Valores de comprimento de coluna específica para cada tipo de dados de intervalo estão contidos no [tamanho da coluna](../../../odbc/reference/appendixes/column-size.md).
