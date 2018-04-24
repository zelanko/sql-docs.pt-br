---
title: Interface ADOStreamConstruction | Microsoft Docs
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
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0be1e9a290fc95303220c9a6c4b80df7e75e2905
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="adostreamconstruction-interface"></a>Interface ADOStreamConstruction
O **ADOStreamConstruction** interface é usada para construir um ADO **fluxo** objeto a partir de um banco de dados OLE **IStream** objeto em um aplicativo C/C++.  
  
## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|[Propriedade Stream](../../../ado/reference/ado-api/stream-property.md)|Leitura/gravação. Obtém/define um banco de dados OLE **fluxo** objeto.|  
  
## <a name="methods"></a>Métodos  
 Nenhuma.  
  
## <a name="events"></a>Eventos  
 Nenhuma.  
  
## <a name="remarks"></a>Remarks  
 Dado um banco de dados OLE **IStream** objeto (`pStream`), a construção de ADO **fluxo** objeto (`adoStr`) de valores para as três operações básicas a seguir:  
  
1.  Criar um ADO **fluxo** objeto:  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  Consulta o **IADOStreamConstruction** interface no **fluxo** objeto:  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 Chamar o `IADOStreamConstruction::get_Stream` método de propriedade para definir o OLE DB **IStream** objeto ADO **fluxo** objeto:  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 O RSoP `adoStr` objeto agora representa o ADO **fluxo** objeto construído a partir do OLE DB **IStream** objeto.  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** ADO 2.0 ou posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API ADO](../../../ado/reference/ado-api/ado-api-reference.md)
