---
title: Interface ADORecordsetConstruction | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ADORecordsetConstruction
helpviewer_keywords: ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bd346172159ac3ee64d2c03a22f2c9a467fc2bcc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="adorecordsetconstruction-interface"></a>Interface ADORecordsetConstruction
O **ADORecordsetConstruction** interface é usada para construir um ADO **registros** objeto a partir de um banco de dados OLE **linhas** objeto em um aplicativo C/C++.  
  
 Esta interface suporta as seguintes propriedades:  
  
## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|[Capítulo](../../../ado/reference/ado-api/chapter-property-ado.md)|Leitura/gravação.<br />Obtém/define um banco de dados OLE **capítulo** objeto de/esse ADO **registros** objeto.|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|Leitura/gravação.<br />Obtém/define um banco de dados OLE **RowPosition** objeto de/esse ADO **registros** objeto.|  
|[Conjunto de linhas](../../../ado/reference/ado-api/rowset-property-ado.md)|Leitura/gravação.<br />Obtém/define um banco de dados OLE **linhas** objeto de/esse ADO **registros** objeto.|  
  
## <a name="methods"></a>Métodos  
 Nenhum.  
  
## <a name="events"></a>Eventos  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 Dado um banco de dados OLE **linhas** objeto (`pRowset`), a construção do ADO **registros** objeto (`adoRs`) de valores para as três operações básicas:  
  
1.  Criar um ADO **registros** objeto:  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  Consulta o **IADORecordsetConstruction** interface no **registros** objeto:  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  Chamar o `IADORecordsetConstruction::put_Rowset` método de propriedade para definir o OLE DB `Rowset` objeto ADO `Recordset` objeto:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 O RSoP `adoRs` objeto agora representa o ADO **registros** objeto construído a partir do OLE DB **linhas** objeto.  
  
 Você também pode construir ADO **registros** objeto a partir de um banco de dados OLE **capítulo** ou **RowPosition** objeto.  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** ADO 2.0 e posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Propriedade Rowset (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
