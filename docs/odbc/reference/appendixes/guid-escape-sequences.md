---
description: Sequências de escape GUID
title: Sequências de escape de GUID | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7babe2d26c0e5f2b311f8df5bbd1763622f3042
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466152"
---
# <a name="guid-escape-sequences"></a>Sequências de escape GUID
O ODBC usa sequências de escape para literais GUID. A sintaxe dessa sequência de escape é a seguinte:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Comentários  
 Na notação BNF, a sintaxe é a seguinte:  
  
 *ODBC-GUID-escape* :: =  
     *ODBC-ESC-GUID do iniciador* '*GUID-Value*' *ODBC-ESC-terminador*  
  
 *ODBC-ESC-Initiator* :: = {  
  
 *ODBC-ESC-terminador* :: =}  
  
 *GUID-valor* :: = *relógio-baixo-valor GUID-tempo de separação de relógio-meio-valor GUID-separador relógio-valor do GUID de alto valor-separador Clock-Seq-valor GUID-Value*  
  
 *GUID-separador* :: =-  
  
 *Clock-baixo-valor* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *Clock-meio-valor* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *relógio-alto valor* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *Clock-Seq-valor* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *Clock-nó-valor* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit* hex_digit hex_digit  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; C &#124; D &#124; E &#124; F  
  
 A sequência de escape literal de GUID terá suporte se o tipo de dados GUID for suportado pela fonte de dados. Um aplicativo deve chamar **SQLGetTypeInfo** para determinar se há suporte para esse tipo de dados.
