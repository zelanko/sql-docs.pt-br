---
description: Cláusulas COMPUTE de forma de intervenção
title: Cláusulas de computação de forma intermediária | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- COMPUTE clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: a576bf81-8f3c-4ba1-817b-87e89a8da684
author: rothja
ms.author: jroth
ms.openlocfilehash: 49393765bfedc832f49fef103ba1076b277277fd
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805891"
---
# <a name="intervening-shape-compute-clauses"></a>Cláusulas COMPUTE de forma de intervenção
É válido inserir uma ou mais cláusulas de computação entre o pai e o filho em um comando de forma com parâmetros, como no exemplo a seguir:  
  
```  
SHAPE {select au_lname, state from authors} APPEND   
   ((SHAPE   
      (SHAPE   
         {select * from authors where state = ?} rs   
      COMPUTE rs, ANY(rs.state) state, ANY(rs.au_lname) au_lname   
      BY au_id) rs2   
   COMPUTE rs2, ANY(rs2.state) BY au_lname)   
RELATE state TO PARAMETER 0)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de formatação de dados](./data-shaping-example.md)   
 [Gramática forma formal](./formal-shape-grammar.md)   
 [Modelar comandos em geral](./shape-commands-in-general.md)