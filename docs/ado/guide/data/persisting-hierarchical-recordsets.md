---
description: Persistência de conjunto de registros hierárquicos
title: Persistindo conjuntos de registros hierárquicos | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4bfcb79e532609ad9b3eeb14fb07dec4fd1239f7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453048"
---
# <a name="persisting-hierarchical-recordsets"></a>Persistência de conjunto de registros hierárquicos
Você pode salvar um **conjunto de registros** hierárquico em um arquivo no formato ADTG ou XML chamando o método [Save](../../../ado/reference/ado-api/save-method.md) . No entanto, duas limitações se aplicam ao salvar o s do **conjunto de registros**hierárquico em formato XML: você não poderá salvar em XML se o **conjunto de registros** hierárquico contiver atualizações pendentes e não for possível salvar um conjunto de **registros**hierárquicos parametrizados.  
  
 Para obter mais informações sobre o provedor de data Shaping, consulte [Microsoft Data Shaping Service for OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) e [visão geral do data shaping Service para OLE DB](https://msdn.microsoft.com/9f51e471-8e85-448e-9fb8-b64bbf767bf3).  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de formatação de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
