---
title: Propriedade Source (registro ADO) | Microsoft Docs
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
ms.openlocfilehash: b1870d8cd8253e1b6de74ce093d51ca6e33c5c6d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67930932"
---
# <a name="source-property-ado-record"></a>Propriedade Source (Registro ADO)
Indica a fonte de dados ou o objeto representado pelo [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um valor **Variant** que indica a entidade representada pelo **registro**.  
  
## <a name="remarks"></a>Comentários  
 A propriedade **Source** retorna o argumento de *origem* do método **Record** [Open](../../../ado/reference/ado-api/open-method-ado-record.md) Object. Ele pode conter uma cadeia de caracteres de URL absoluta ou relativa. Uma URL absoluta pode ser usada sem definir a propriedade [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) para abrir diretamente o objeto **Record** . Um objeto de **conexão** implícita é criado nesse caso.  
  
 A propriedade **Source** também pode conter uma referência a um conjunto de **registros**já aberto, que abre um objeto de **registro** que representa a linha atual no **conjunto de registros**.  
  
 A propriedade **Source** também pode conter uma referência a um objeto [Command](../../../ado/reference/ado-api/command-object-ado.md) que retorna uma única linha de dados do provedor.  
  
 Se a propriedade **ActiveConnection** também for definida, a propriedade **Source** deverá apontar para algum objeto que existe dentro do escopo dessa conexão. Por exemplo, em namespaces estruturados em árvore, se a propriedade **Source** contiver uma URL absoluta, ela deverá apontar para um nó que existe dentro do escopo do nó identificado pela URL na cadeia de conexão. Se a propriedade **Source** contiver uma URL relativa, ela será validada dentro do contexto definido pela propriedade **ActiveConnection** .  
  
 A propriedade de **origem** é leitura/gravação enquanto o objeto de **registro** é fechado e é somente leitura enquanto o objeto de **registro** está aberto.  
  
> [!NOTE]
>  As URLs que usam o esquema http invocarão automaticamente o [provedor do Microsoft OLE DB para publicação na Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obter mais informações, consulte [URLs absolutas e relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedade Source (erro ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [Propriedade Source (Conjunto de registros ADO)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
