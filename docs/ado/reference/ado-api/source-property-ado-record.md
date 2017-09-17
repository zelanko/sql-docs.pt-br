---
title: Propriedade (registro de ADO) de origem | Microsoft Docs
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
- _Record::Source
- _Record::PutRefSource
- _Record::GetSource
- _Record::put_Source
- _Record::putref_Source
- _Record::get_Source
helpviewer_keywords:
- Source property [ADO Record]
ms.assetid: 2c18279e-6f35-4af0-b12e-8f1543d9ed20
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 524845f59338a483df89586847157e6d9eaa598c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="source-property-ado-record"></a>Propriedade Source (ADO registro)
Indica a fonte de dados ou o objeto representado pelo [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um **Variant** valor que indica a entidade representada pelo **registro**.  
  
## <a name="remarks"></a>Comentários  
 O **fonte** propriedade retorna o *fonte* argumento do **registro** objeto [abrir](../../../ado/reference/ado-api/open-method-ado-record.md) método. Ele pode conter uma cadeia de caracteres de URL absoluta ou relativa. Uma URL absoluta que pode ser usada sem configuração o [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propriedade abrir diretamente o **registro** objeto. Implícita **Conexão** objeto é criado nesse caso.  
  
 O **fonte** propriedade também pode conter uma referência a uma já aberto **registros**, que abre um **registro** objeto que representa a linha atual o ** Conjunto de registros**.  
  
 O **fonte** propriedade também pode conter uma referência a um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que retorna uma única linha de dados do provedor.  
  
 Se o **ActiveConnection** propriedade também é definida, o **fonte** propriedade deve apontar para um objeto que existe dentro do escopo dessa conexão. Por exemplo, em namespaces estruturados em árvore, se o **fonte** propriedade contém uma URL absoluta, ela deve apontar para um nó que existe dentro do escopo do nó identificado por URL na cadeia de conexão. Se o **fonte** propriedade contém uma URL relativa, em seguida, ela é validada no contexto definido pelo **ActiveConnection** propriedade.  
  
 O **fonte** propriedade é leitura/gravação ao **registro** objeto é fechado e é somente leitura enquanto o **registro** objeto está aberto.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [Absolute e URLs relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Source (erro de ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Propriedade Source (Conjunto de registros ADO)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
