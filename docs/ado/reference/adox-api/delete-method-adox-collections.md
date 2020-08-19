---
description: Método Delete (Coleções do ADOX)
title: Método Delete (coleções do ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::Delete
- Groups::Delete
- Indexes::raw_Delete
- Columns::raw_Delete
- Tables::Delete
- Keys::Delete
- Users::Delete
- Users::raw_Delete
- Keys::raw_Delete
- Procedures::raw_Delete
- Views::raw_Delete
- Indexes::Delete
- Procedures::Delete
- Groups::raw_Delete
- Tables::raw_Delete
- Columns::Delete
helpviewer_keywords:
- delete method [ADOX]
ms.assetid: e6b6e3a4-8952-4d79-81f4-51019c338374
author: rothja
ms.author: jroth
ms.openlocfilehash: 7345337ab35f4154fd9dc53f749e04dba96dad48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440108"
---
# <a name="delete-method-adox-collections"></a>Método Delete (Coleções do ADOX)
Remove um objeto de uma coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Uma **variante** que especifica o nome ou a posição ordinal (índice) do objeto a ser excluído.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o *nome* não existir na coleção.  
  
 Para coleções de [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) e [usuários](../../../ado/reference/adox-api/users-collection-adox.md) , ocorrerá um erro se o provedor não der suporte à exclusão de tabelas ou usuários, respectivamente. Para [procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md) e coleções de [modos de exibição](../../../ado/reference/adox-api/views-collection-adox.md) , a **exclusão** falhará se o provedor não oferecer suporte a comandos persistentes.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
        [Coleção Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
        [Coleção Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
        [Coleção Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)  
        [Coleção Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
        [Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Delete de procedimentos (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Exemplo do método Delete de exibições (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
