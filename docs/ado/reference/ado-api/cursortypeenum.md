---
title: CursorTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4da9f1f931a9f6d15c5b0e13959f0e9effd40bcc
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="cursortypeenum"></a>CursorTypeEnum
Especifica o tipo de cursor usado em uma [registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|Usa um cursor dinâmico. Adições, alterações e exclusões por outros usuários são visíveis e todos os tipos de movimento por meio de **registros** são permitidas, exceto para indicadores, se o provedor não oferecer suporte a eles.|  
|**adOpenForwardOnly**|0|Padrão. Usa um cursor somente de avanço. Idêntico a um cursor estático, exceto que você só pode rolar para frente por meio de registros. Isso melhora o desempenho quando você precisa fazer somente uma passagem um **registros**.|  
|**adOpenKeyset**|1|Usa um cursor de conjunto de chaves. Como um cursor dinâmico, exceto que não é possível ver os registros que adicionarem outros usuários, embora os registros que outros usuários excluírem podem ser acessados da sua **registros**. Alterações de dados por outros usuários estão visíveis.|  
|**adOpenStatic**|3|Usa um cursor estático, o que é uma cópia estática de um conjunto de registros que você pode usar para encontrar dados ou gerar relatórios. Adições, alterações ou exclusões por outros usuários não são visíveis.|  
|**adOpenUnspecified**|-1|Não especifique o tipo de cursor.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC equivalente  
 Pacote: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CursorType.DYNAMIC|  
|AdoEnums.CursorType.FORWARDONLY|  
|AdoEnums.CursorType.KEYSET|  
|AdoEnums.CursorType.STATIC|  
|AdoEnums.CursorType.UNSPECIFIED|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
