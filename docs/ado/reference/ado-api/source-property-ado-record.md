---
title: Propriedade (registro ADO) de origem | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9217658a645d731645b0c85a419ecf759b1fd3bb
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711111"
---
# <a name="source-property-ado-record"></a>Propriedade Source (Registro ADO)
Indica a fonte de dados ou o objeto representado pelo [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="settings-and-return-values"></a>As configurações e valores de retorno  
 Define ou retorna um **Variant** valor que indica a entidade representada pela **registro**.  
  
## <a name="remarks"></a>Comentários  
 O **fonte** propriedade retorna o *fonte* argumento do **registro** objeto [abrir](../../../ado/reference/ado-api/open-method-ado-record.md) método. Ele pode conter uma cadeia de caracteres de URL absoluta ou relativa. Uma URL absoluta que pode ser usada sem definir a [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) para abrir diretamente o **registro** objeto. Implícito **Conexão** objeto é criado nesse caso.  
  
 O **fonte** propriedade também pode conter uma referência a uma já aberta **conjunto de registros**, que abre uma **registro** objeto que representa a linha atual do  **Conjunto de registros**.  
  
 O **fonte** propriedade também pode conter uma referência a um [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto que retorna uma única linha de dados do provedor.  
  
 Se o **ActiveConnection** propriedade também é definida, o **origem** propriedade deve apontar para algum objeto que existe dentro do escopo dessa conexão. Por exemplo, nos namespaces estruturados em árvore, se o **origem** propriedade contém uma URL absoluta, ele deve apontar para um nó que existe dentro do escopo do nó identificado pela URL na cadeia de conexão. Se o **fonte** propriedade contém uma URL relativa, em seguida, ele é validado no contexto definido pela **ActiveConnection** propriedade.  
  
 O **fonte** propriedade é leitura/gravação, enquanto o **registro** objeto está fechado e é somente leitura enquanto o **registro** objeto está aberto.  
  
> [!NOTE]
>  URLs usando o esquema http invocará automaticamente o [Microsoft OLE DB Provider para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [absoluta e relativa URLs](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade Source (Erro ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Propriedade Source (Conjunto de registros ADO)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
