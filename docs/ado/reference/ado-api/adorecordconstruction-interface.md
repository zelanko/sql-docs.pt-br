---
title: Interface ADORecordConstruction | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3966038215e1d26828d60b739ac6060859eabd67
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="adorecordconstruction-interface"></a>Interface ADORecordConstruction
O **ADORecordConstruction**interface é usada para construir um ADO **registro** objeto a partir de um banco de dados OLE **linha** objeto em um aplicativo C/C++.  
  
 Esta interface suporta as seguintes propriedades:  
  
## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|Somente gravação.<br />Define o contêiner do OLE DB **linha** objeto este ADO **registro** objeto.|  
|[Linha](../../../ado/reference/ado-api/row-property-ado.md)|Leitura/gravação.<br />Obtém/define um banco de dados OLE **linha** objeto de/esse ADO **registro** objeto.|  
  
## <a name="methods"></a>Métodos  
 Nenhum.  
  
## <a name="events"></a>Eventos  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 Dado um OLE DB **linha** objeto (`pRow`), a construção de ADO **registro** objeto (`adoR`), valores para as três operações básicas a seguir:  
  
1.  Criar um ADO **registro** objeto:  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  Consulta o **IADORecordConstruction** interface no **registro** objeto:  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  Chamar o **IADORecordConstruction::put_Row** método de propriedade para definir o OLE DB **linha** objeto ADO **registro** objeto:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 O RSoP **objeto adoR** objeto agora representa o ADO **registro** objeto construído a partir do OLE DB **linha** objeto.  
  
 ADO **registro** objeto também pode ser construído do contêiner do OLE DB **linha** objeto.  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** ADO 2.0 e posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4

