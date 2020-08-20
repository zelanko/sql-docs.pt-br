---
description: Comandos híbridos
title: Comandos híbridos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- hybrid commands [ADO]
- data shaping [ADO], hybrid commands
ms.assetid: e8ca40e8-459c-40e2-8dd3-3ec6d5ee7b51
author: rothja
ms.author: jroth
ms.openlocfilehash: d3c6a852f5918a79c0fb2df5e2f60ef415cca6a1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453238"
---
# <a name="hybrid-commands"></a>Comandos híbridos
Os comandos híbridos são comandos parcialmente parametrizados. Por exemplo:   
  
```  
SHAPE {select * from plants}   
   APPEND( {select * from customers where country = ?}   
           RELATE PlantCountry TO PARAMETER 0,   
             PlantRegion TO CustomerRegion )   
```  
  
 O comportamento de caching para um comando híbrido é o mesmo dos comandos regulares com parâmetros.  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de formatação de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
