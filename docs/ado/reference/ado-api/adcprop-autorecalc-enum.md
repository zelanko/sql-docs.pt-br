---
description: ADCPROP_AUTORECALC_ENUM
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e0b9cf745ae30d11d85aeba1c916594e09392c6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451608"
---
# <a name="adcprop_autorecalc_enum"></a>ADCPROP_AUTORECALC_ENUM
Especifica quando o provedor [MSDataShape](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) recalcula as colunas agregadas e calculadas em um conjunto de registros hierárquico.  
  
 Essas constantes são usadas apenas com o **provedor MSDataShape** e a propriedade dinâmica **"recálculo automático**" do **conjunto de registros** , que é referenciada no índice de [propriedade dinâmica do ADO](../../../ado/reference/ado-api/ado-dynamic-property-index.md) e documentada no [serviço de cursor da Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) ou [o serviço de modelagem de dados da Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) documentação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Padrão. Recalcula sempre que o provedor **MSDataShape** determina valores que as colunas calculadas dependem de terem mudado.|  
|**adRecalcUpFront**|0|Calcula somente ao criar inicialmente o conjunto de **registros**hierárquico.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.
