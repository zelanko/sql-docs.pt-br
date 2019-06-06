---
title: CursorTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorTypeEnum
helpviewer_keywords:
- CursorTypeEnum enumeration [ADO]
ms.assetid: ffc6e245-4471-42ae-84dd-e85bddfce983
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: dd3469b826ac4f577ff0e883b1a92a3acec4a981
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698538"
---
# <a name="cursortypeenum"></a>CursorTypeEnum
Especifica o tipo de cursor usado em uma [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adOpenDynamic**|2|Usa um cursor dinâmico. Adições, alterações e exclusões por outros usuários estão visíveis e todos os tipos de movimento por meio de **conjunto de registros** são permitidos, exceto para os marcadores, se o provedor não dá suporte a eles.|  
|**adOpenForwardOnly**|0|Padrão. Usa um cursor de somente avanço. Idêntico a um cursor estático, exceto que você só pode navegar para frente por meio de registros. Isso melhora o desempenho quando você precisa fazer apenas uma passar por uma **conjunto de registros**.|  
|**adOpenKeyset**|1|Usa um cursor keyset. Como um cursor dinâmico, exceto que você não pode ver os registros que adicionarem outros usuários, embora os registros que outros usuários excluem estão inacessíveis de sua **conjunto de registros**. As alterações de dados por outros usuários ainda estarão visíveis.|  
|**adOpenStatic**|3|Usa um cursor estático, que é uma cópia estática de um conjunto de registros que você pode usar para localizar os dados ou gerar relatórios. Adições, alterações ou exclusões por outros usuários não são visíveis.|  
|**adOpenUnspecified**|-1|Não especifica o tipo de cursor.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Package: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CursorType.DYNAMIC|  
|AdoEnums.CursorType.FORWARDONLY|  
|AdoEnums.CursorType.KEYSET|  
|AdoEnums.CursorType.STATIC|  
|AdoEnums.CursorType.UNSPECIFIED|  
  
## <a name="applies-to"></a>Aplica-se a  
 [Propriedade CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
