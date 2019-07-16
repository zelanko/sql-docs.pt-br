---
title: Interface ADOStreamConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70a6dd02722a34159b345a83b32897aa8c38d0ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920783"
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction Interface
O **ADOStreamConstruction** interface é usada para construir o ADO **Stream** objeto a partir de um banco de dados OLE **IStream** objeto em um aplicativo C/C++.  
  
## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|[Propriedade Stream](../../../ado/reference/ado-api/stream-property.md)|Leitura/gravação. Obtém/define um banco de dados OLE **Stream** objeto.|  
  
## <a name="methods"></a>Métodos  
 nenhuma.  
  
## <a name="events"></a>Events  
 nenhuma.  
  
## <a name="remarks"></a>Comentários  
 Dado um banco de dados OLE **IStream** objeto (`pStream`), a construção de ADO **Stream** objeto (`adoStr`) de valores para as três operações básicas a seguir:  
  
1.  Criar um ADO **Stream** objeto:  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  Consulta a **IADOStreamConstruction** interface sobre o **Stream** objeto:  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 Chame o `IADOStreamConstruction::get_Stream` método de propriedade para definir o banco de dados OLE **IStream** objeto ADO **Stream** objeto:  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 O resultante `adoStr` objeto agora representa o ADO **Stream** objeto construído a partir do OLE DB **IStream** objeto.  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** O ADO 2.0 ou posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API ADO](../../../ado/reference/ado-api/ado-api-reference.md)
