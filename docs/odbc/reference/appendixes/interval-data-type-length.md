---
title: Comprimento do tipo de dados do intervalo | Microsoft Docs
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
ms.openlocfilehash: a456db12ddb2594dc7b4c9e4f5c26e9cb4245621
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67947592"
---
# <a name="interval-data-type-length"></a>Comprimento do tipo de dados de intervalo
As regras a seguir são usadas para determinar o comprimento de um tipo de dados de intervalo em caracteres. O comprimento é expresso em número de caracteres. O número de bytes depende do conjunto de caracteres. O comprimento inclui os seguintes valores adicionados juntos:  
  
-   Dois caracteres para cada campo no intervalo que não é o campo à esquerda.  
  
-   Para o campo principal, o número de caracteres que é a precisão inicial expressa ou implícita. Se a precisão à esquerda não for especificada, o valor padrão será 2.  
  
-   Um caractere para o separador entre os campos.  
  
-   Uma além da precisão de segundos expressos ou implícitas. Se a precisão de segundos não for especificada, o valor padrão será 6.  
  
 Os valores de comprimento de coluna específicos para cada tipo de dados de intervalo estão contidos no [tamanho da coluna](../../../odbc/reference/appendixes/column-size.md).
