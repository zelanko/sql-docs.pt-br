---
title: Propriedade StayInSync | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::StayInSync
- Recordset20::put_StayInSync
- Recordset20::PutStayInSync
- Recordset20::get_StayInSync
- Recordset20::GetStayInSync
helpviewer_keywords:
- StayInSync property
ms.assetid: 502d69b5-dc9a-455d-b115-a03bd39a552b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50cf569f6e0af5e753cca7fba030b8fc2caa4a86
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743122"
---
# <a name="stayinsync-property"></a>Propriedade StayInSync
Indica, em modo hierárquico [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objeto, se a referência para os registros filho subjacente (ou seja, o *capítulo*) é alterado quando a linha pai posicione as alterações.  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **Boolean** valor. O valor padrão é **True**. Se **verdadeira**, o capítulo será atualizado se pai **conjunto de registros** alterações do objeto de linha posição; se **False**, o capítulo continuará se referem aos dados no capítulo anterior mesmo que o pai **Recordset** objeto foi alterado a posição da linha.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade aplica-se a conjuntos de registros hierárquicos, como aqueles compatíveis com o [Microsoft Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)e deve ser definido no pai **conjunto de registros** antes do filho  **Conjunto de registros** é recuperado. Essa propriedade simplifica navegando conjuntos de registros hierárquicos.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade StayInSync (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Microsoft Data Shaping Service para OLE DB (provedor de serviços do ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
