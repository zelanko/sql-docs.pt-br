---
description: ADCPROP_AUTORECALC_ENUM
title: ADCPROP_AUTORECALC_ENUM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 571d3eb0d8d836a96b2f3f7a79807bd2d2c16fdf
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976837"
---
# <a name="adcprop_autorecalc_enum"></a>ADCPROP_AUTORECALC_ENUM
Especifica quando o provedor [MSDataShape](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) recalcula as colunas agregadas e calculadas em um conjunto de registros hierárquico.  
  
 Essas constantes são usadas apenas com o **provedor MSDataShape** e a propriedade dinâmica **"recálculo automático**" do **conjunto de registros** , que é referenciada no índice de [propriedade dinâmica do ADO](./ado-dynamic-property-index.md) e documentada no [serviço de cursor da Microsoft para OLE DB](../../guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) ou [o serviço de modelagem de dados da Microsoft para OLE DB](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) documentação.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adRecalcAlways**|1|Padrão. Recalcula sempre que o provedor **MSDataShape** determina valores que as colunas calculadas dependem de terem mudado.|  
|**adRecalcUpFront**|0|Calcula somente ao criar inicialmente o conjunto de **registros**hierárquico.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Essas constantes não têm equivalentes ADO/WFC.