---
title: Interface ADORecordsetConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction
helpviewer_keywords:
- ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
author: rothja
ms.author: jroth
ms.openlocfilehash: 770bf86f62f243ea255693c7773e6fae48527cfd
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747082"
---
# <a name="adorecordsetconstruction-interface"></a>Interface ADORecordsetConstruction
A interface **ADORecordsetConstruction** é usada para construir um objeto **Recordset** ado de um objeto **conjunto de linhas** OLE DB em um aplicativo C/C++.  
  
 Esta interface dá suporte às seguintes propriedades:  
  
## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|[Capítulo](../../../ado/reference/ado-api/chapter-property-ado.md)|Leitura/gravação.<br />Obtém/define um OLE DB objeto de **capítulo** de/neste objeto ADO **Recordset** .|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|Leitura/gravação.<br />Obtém/define um OLE DB objeto de **função** de/neste objeto ADO **Recordset** .|  
|[Conjunto de linhas](../../../ado/reference/ado-api/rowset-property-ado.md)|Leitura/gravação.<br />Obtém/define um OLE DB objeto de **conjunto de linhas** de/neste objeto ADO **Recordset** .|  
  
## <a name="methods"></a>Métodos  
 Nenhum.  
  
## <a name="events"></a>Eventos  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 Dado um OLE DB objeto de **conjunto de linhas** ( `pRowset` ), a construção de um objeto **Recordset** ADO ( `adoRs` ) resulta em três operações básicas a seguir:  
  
1.  Criar um objeto ADO **Recordset** :  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  Consulte a interface **IADORecordsetConstruction** no objeto **Recordset** :  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  Chame o `IADORecordsetConstruction::put_Rowset` método Property para definir o OLE DB `Rowset` objeto no objeto ADO `Recordset` :  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 O objeto resultante `adoRs` agora representa o objeto **Recordset** ADO construído a partir do objeto de **conjunto de linhas** OLE DB.  
  
 Você também pode construir um objeto **RECORDSET** ado a partir de um OLE DB **capítulo** ou objeto de uma **posição** .  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** ADO 2,0 e posterior  
  
 **Biblioteca:** MsADO15. dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Propriedade Rowset (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
