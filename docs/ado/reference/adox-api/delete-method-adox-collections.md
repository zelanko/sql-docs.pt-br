---
title: Excluir método (coleções do ADOX) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90f9aa6a788296ff5fef05e96b7f46b56729ded9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298477"
---
# <a name="delete-method-adox-collections"></a>Método Delete (Coleções do ADOX)
Remove um objeto de uma coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Nome*  
 Um **Variant** que especifica o nome ou posição ordinal (índice) do objeto a ser excluído.  
  
## <a name="remarks"></a>Comentários  
 Ocorrerá um erro se o *nome* não existe na coleção.  
  
 Para [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) e [usuários](../../../ado/reference/adox-api/users-collection-adox.md) coleções, ocorrerá um erro se o provedor não dá suporte a exclusão de tabelas ou usuários, respectivamente. Para [procedimentos](../../../ado/reference/adox-api/procedures-collection-adox.md) e [exibições](../../../ado/reference/adox-api/views-collection-adox.md) coleções **excluir** falhará se o provedor não dá suporte a comandos de persistência.  
  
## <a name="applies-to"></a>Aplica-se a  
  
||||  
|-|-|-|  
|[Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Coleção Groups (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Coleção Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Coleção Procedures (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Coleção Tables (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Coleção Users (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Coleção Views (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>Consulte também  
 [Delete de procedimentos de exemplo do método (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Exemplo do método Delete de exibições (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
