---
title: Método (índices do ADOX) append | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18e9162c3c9a1b79c28ca6e0ae94f8680db0ac80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206256"
---
# <a name="append-method-adox-indexes"></a>Método Append (Índices do ADOX)
Adiciona um novo [índice](../../../ado/reference/adox-api/index-object-adox.md) do objeto para o [índices](../../../ado/reference/adox-api/indexes-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Index*  
 O **índice** objeto a ser acrescentado ou o nome do índice para criar e anexar.  
  
 *Colunas*  
 Opcional. Um **Variant** valor que especifica os nomes de colunas a serem indexados. O *colunas* parâmetro corresponde do valor (es) da [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade de um [coluna](../../../ado/reference/adox-api/column-object-adox.md) ou mais objetos.  
  
## <a name="remarks"></a>Comentários  
 O *colunas* parâmetro pode assumir o nome de uma coluna ou uma matriz de nomes de coluna.  
  
 Se o provedor não dá suporte a criação de índices, ocorrerá um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo (VB) do método Indexes Append](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Acrescentar o método (colunas do ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Acrescentar o método (grupos do ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Acrescentar o método (chaves do ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescentar o método (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Acrescentar o método (tabelas do ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Acrescentar o método (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
