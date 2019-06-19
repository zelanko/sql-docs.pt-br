---
title: Manter conjuntos de registros hierárquicos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f25b61ca54b3a4ac15584ecf31874f90787c735d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700462"
---
# <a name="persisting-hierarchical-recordsets"></a>Persistência de conjunto de registros hierárquicos
Você pode salvar um hierárquica **conjunto de registros** em um arquivo no formato ADTG ou XML, chamando o [salvar](../../../ado/reference/ado-api/save-method.md) método. No entanto, duas limitações se aplicam ao salvar hierárquica **Recordset**s em formato XML: Não é possível salvar em XML se o hierárquica **conjunto de registros** contém as atualizações pendentes, e não é possível salvar um parametrizada hierárquica **conjunto de registros**.  
  
 Para obter mais informações sobre o provedor de dados de formatação, consulte [Microsoft Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) e [visão geral de Data Shaping Service para OLE DB](https://msdn.microsoft.com/9f51e471-8e85-448e-9fb8-b64bbf767bf3).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
