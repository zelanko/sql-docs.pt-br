---
description: ADOStreamConstruction Interface
title: Interface ADOStreamConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f6e32b076fa0faa43a3dff46aed66bcadaa2f1ae
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976157"
---
# <a name="adostreamconstruction-interface"></a>ADOStreamConstruction Interface
A interface **ADOStreamConstruction** é usada para construir um objeto de **fluxo** ADO de um objeto OLE DB **IStream** em um aplicativo C/C++.  
  
## <a name="properties"></a>Propriedades  
  
|Propriedade|Descrição|  
|-|-|  
|[Fluxo](./stream-property.md)|Leitura/gravação. Obtém/define um objeto de **fluxo** de OLE DB.|  
  
## <a name="methods"></a>Métodos  
 Nenhum.  
  
## <a name="events"></a>Eventos  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 Dado um OLE DB objeto **IStream** ( `pStream` ), a construção de um objeto de **fluxo** ADO ( `adoStr` ) é quantiada para as três operações básicas a seguir:  
  
1.  Criar um objeto de **fluxo** ADO:  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  Consulte a interface **IADOStreamConstruction** no objeto **Stream** :  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 Chame o `IADOStreamConstruction::get_Stream` método Property para definir o objeto OLE DB **IStream** no objeto de **fluxo** ADO:  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 O objeto resultante `adoStr` agora representa o objeto de **fluxo** ADO construído a partir do objeto OLE DB **IStream** .  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** ADO 2,0 ou uma versão posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API ADO](./ado-api-reference.md)