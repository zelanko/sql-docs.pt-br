---
description: Método Delete (Coleções do ADOX)
title: Método Delete (coleções do ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: e92cbe56bb7823b5c6cfd2485d887f3e3c56a8e5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984617"
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
  
 Para coleções de [tabelas](./tables-collection-adox.md) e [usuários](./users-collection-adox.md) , ocorrerá um erro se o provedor não der suporte à exclusão de tabelas ou usuários, respectivamente. Para [procedimentos](./procedures-collection-adox.md) e coleções de [modos de exibição](./views-collection-adox.md) , a **exclusão** falhará se o provedor não oferecer suporte a comandos persistentes.  
  
## <a name="applies-to"></a>Aplica-se A  

:::row:::
    :::column:::
        [Coleção Columns (ADOX)](./columns-collection-adox.md)  
        [Coleção Groups (ADOX)](./groups-collection-adox.md)  
        [Coleção Indexes (ADOX)](./indexes-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Coleção Keys (ADOX)](./keys-collection-adox.md)  
        [Coleção Procedures (ADOX)](./procedures-collection-adox.md)  
        [Coleção Tables (ADOX)](./tables-collection-adox.md)  
    :::column-end:::
    :::column:::
        [Coleção Users (ADOX)](./users-collection-adox.md)  
        [Coleção Views (ADOX)](./views-collection-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [Exemplo do método Delete de procedimentos (VB)](./procedures-delete-method-example-vb.md)   
 [Exemplo do método Delete de exibições (VB)](./views-delete-method-example-vb.md)