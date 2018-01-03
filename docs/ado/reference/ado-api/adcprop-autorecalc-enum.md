---
title: ADCPROP_AUTORECALC_ENUM | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ADCPROP_AUTORECALC_ENUM
helpviewer_keywords: ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0be561a70465aab4483fc3a2e870cbc9b68972b8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="adcpropautorecalcenum"></a>ADCPROP_AUTORECALC_ENUM
Especifica quando o [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) provedor calcula novamente colunas calculadas e agregação em um conjunto de registros hierárquico.  
  
 Essas constantes são usadas apenas com o **MSDataShape** provedor e o **registros** "**recálculo automático**" propriedade dinâmica, que é referenciada no [ADO Índice de propriedade dinâmica](../../../ado/reference/ado-api/ado-dynamic-property-index.md) e documentado o [do serviço Microsoft Cursor do OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) ou [Microsoft Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) documentação.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Padrão. Recalcula sempre que o **MSDataShape** provedor determina os valores que dependem de colunas calculadas que foram alterados.|  
|**adRecalcUpFront**|0|Calcula apenas quando criar inicialmente o hierárquica **registros**.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Constantes não têm equivalentes do ADO/WFC.
