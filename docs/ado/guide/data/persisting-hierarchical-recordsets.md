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
manager: craigg
ms.openlocfilehash: 2db4e4b4d3d7d137f4f033e35dd643cb0a2d11bb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666624"
---
# <a name="persisting-hierarchical-recordsets"></a>Persistência de conjunto de registros hierárquicos
Você pode salvar um hierárquica **conjunto de registros** em um arquivo no formato ADTG ou XML, chamando o [salvar](../../../ado/reference/ado-api/save-method.md) método. No entanto, duas limitações se aplicam ao salvar hierárquica **conjunto de registros**s em formato XML: não é possível salvar em XML se o hierárquica **Recordset** contém as atualizações pendentes, e não é possível salvar um com parâmetros hierárquica **conjunto de registros**.  
  
 Para obter mais informações sobre o provedor de dados de formatação, consulte [Microsoft Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) e [visão geral de Data Shaping Service para OLE DB](http://msdn.microsoft.com/9f51e471-8e85-448e-9fb8-b64bbf767bf3).  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
