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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e1d14255acd4cc7f18abea1c494353ef970903c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920792"
---
# <a name="adorecordsetconstruction-interface"></a>Interface ADORecordsetConstruction
A interface **ADORecordsetConstruction** é usada para construir um objeto **Recordset** ado de um objeto **conjunto de linhas** OLE DB em um aplicativo C/C++.  
  
 Esta interface dá suporte às seguintes propriedades:  
  
## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|[Capítulo](../../../ado/reference/ado-api/chapter-property-ado.md)|Leitura/gravação.<br />Obtém/define um OLE DB objeto de **capítulo** de/neste objeto ADO **Recordset** .|  
|[Colocar](../../../ado/reference/ado-api/rowposition-property-ado.md)|Leitura/gravação.<br />Obtém/define um OLE DB objeto de **função** de/neste objeto ADO **Recordset** .|  
|[Conjunto de linhas](../../../ado/reference/ado-api/rowset-property-ado.md)|Leitura/gravação.<br />Obtém/define um OLE DB objeto de **conjunto de linhas** de/neste objeto ADO **Recordset** .|  
  
## <a name="methods"></a>Métodos  
 Nenhum.  
  
## <a name="events"></a>Eventos  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 Dado um OLE DB objeto de conjunto`pRowset`de **linhas** (), a construção de um objeto`adoRs` **Recordset** ADO () resulta em três operações básicas a seguir:  
  
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
  
 O `adoRs` objeto resultante agora representa o objeto **Recordset** ADO construído a partir do objeto de **conjunto de linhas** OLE DB.  
  
 Você também pode construir um objeto **RECORDSET** ado a partir de um OLE DB **capítulo** ou objeto de uma **posição** .  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** ADO 2,0 e posterior  
  
 **Biblioteca:** MsADO15. dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Propriedade Rowset (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
