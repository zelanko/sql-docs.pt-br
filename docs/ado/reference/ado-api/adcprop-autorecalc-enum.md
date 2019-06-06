---
title: ADCPROP_AUTORECALC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADCPROP_AUTORECALC_ENUM
helpviewer_keywords:
- ADCPROP_AUTORECALC_ENUM [ADO]
ms.assetid: ded4f087-87b9-4efa-8026-bde53d3e9e8a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c3c085a09b800bb5dd6ce02ca3fa2d570b74190e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718575"
---
# <a name="adcpropautorecalcenum"></a>ADCPROP_AUTORECALC_ENUM
Especifica quando o [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) provedor calcula novamente colunas agregadas e calculadas em um conjunto de registros hierárquico.  
  
 Essas constantes são usadas apenas com o **MSDataShape** provedor e o **conjunto de registros** "**recálculo automático**" propriedade dinâmica, que é referenciada no [ADO A propriedade dinâmica de índice](../../../ado/reference/ado-api/ado-dynamic-property-index.md) e está documentado a [Microsoft Cursor Service para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) ou [Microsoft Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) documentação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Padrão. Recalcula sempre que o **MSDataShape** provedor determina os valores que dependem de colunas calculadas que foram alterados.|  
|**adRecalcUpFront**|0|Calcula apenas quando criar inicialmente o hierárquica **conjunto de registros**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes do ADO/WFC.
