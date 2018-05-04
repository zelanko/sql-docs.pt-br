---
title: Conjuntos de registros hierárquicos persistentes | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1506bd80eee82c2b93a3f3f543825efef394ef07
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="persisting-hierarchical-recordsets"></a>Conjuntos de registros hierárquicos persistentes
Você pode salvar um hierárquica **registros** para um arquivo no formato ADTG ou XML, chamando o [salvar](../../../ado/reference/ado-api/save-method.md) método. No entanto, duas limitações se aplicam ao salvar hierárquica **registros**s em formato XML: não é possível salvar em XML se o hierárquica **registros** contém as atualizações pendentes, e não é possível salvar um com parâmetros hierárquica **registros**.  
  
 Para obter mais informações sobre o provedor de dados de formatação, consulte [Microsoft Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) e [visão geral do Data Shaping Service para OLE DB](http://msdn.microsoft.com/en-us/9f51e471-8e85-448e-9fb8-b64bbf767bf3).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelagem de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
