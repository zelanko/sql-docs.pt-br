---
title: "Método (ADOX índices) append | Microsoft Docs"
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
- Indexes::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 6695769f-275b-4b70-81bd-1a5f7d74926c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb25d4ce8ab95f1311460f67b79a2b2199b96e62
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-indexes"></a>Método (ADOX índices) append
Adiciona um novo [índice](../../../ado/reference/adox-api/index-object-adox.md) o objeto para o [índices](../../../ado/reference/adox-api/indexes-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Indexes.Append Index [,Columns]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Índice*  
 O **índice** objeto a ser acrescentado ou o nome do índice para criar e anexar.  
  
 *Colunas*  
 Opcional. Um **Variant** valor que especifica os nomes das colunas a serem indexados. O *colunas* parâmetro corresponde para os valores da [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade de um [coluna](../../../ado/reference/adox-api/column-object-adox.md) objeto ou objetos.  
  
## <a name="remarks"></a>Comentários  
 O *colunas* parâmetro pode ser o nome de uma coluna ou uma matriz de nomes de coluna.  
  
 Se o provedor não oferece suporte a criação de índices, ocorrerá um erro.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Indexes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Índices de acrescentar o exemplo de método (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Acrescente o método (ADOX colunas)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [(Grupos de ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [(ADOX chaves) do método append](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescente o método (ADOX procedimentos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [(Tabelas ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Acrescente o método (ADOX usuários)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
