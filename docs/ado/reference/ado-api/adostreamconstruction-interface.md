---
title: Interface ADOStreamConstruction | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ADOStreamConstruction
helpviewer_keywords: ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 58d8769837d186f3e9bc1decc9559cf39cb22ec8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="adostreamconstruction-interface"></a>Interface ADOStreamConstruction
O **ADOStreamConstruction** interface é usada para construir um ADO **fluxo** objeto a partir de um banco de dados OLE **IStream** objeto em um aplicativo C/C++.  
  
## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|[Propriedade Stream](../../../ado/reference/ado-api/stream-property.md)|Leitura/gravação. Obtém/define um banco de dados OLE **fluxo** objeto.|  
  
## <a name="methods"></a>Métodos  
 Nenhum.  
  
## <a name="events"></a>Eventos  
 Nenhum.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API ADO](../../../ado/reference/ado-api/ado-api-reference.md)
