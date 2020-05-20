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
author: rothja
ms.author: jroth
ms.openlocfilehash: f36eace18280cd810341c5eeeec1fb294999e6ec
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759632"
---
# <a name="stayinsync-property"></a>Propriedade StayInSync
Indica, em um objeto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) hierárquico, se a referência aos registros filho subjacentes (ou seja, o *capítulo*) é alterada quando a posição da linha pai é alterada.  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **booliano** . O valor padrão é **True**. Se **for true**, o capítulo será atualizado se o objeto do **conjunto de registros** pai alterar a posição da linha; Se **for false**, o capítulo continuará a se referir aos dados no capítulo anterior, mesmo que o objeto **Recordset** pai tenha alterado a posição da linha.  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade se aplica a conjuntos de registros hierárquicos, como aqueles com suporte do [Microsoft Data Shaping Service para OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)e deve ser definida no **conjunto de registros** pai antes da recuperação do **conjunto de registros** filho. Essa propriedade simplifica a navegação de conjuntos de registros hierárquicos.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade StayInSync (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Serviço de modelagem de dados da Microsoft para OLE DB (provedor de serviços ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
