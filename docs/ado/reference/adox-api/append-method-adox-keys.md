---
title: "Método (ADOX chaves) append | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Keys::Append
- Keys::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5821bdda7ae3276d8da83267de45ba46ad6bfbb
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-keys"></a>(ADOX chaves) do método append
Adiciona um novo [chave](../../../ado/reference/adox-api/key-object-adox.md) o objeto para o [chaves](../../../ado/reference/adox-api/keys-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Chave*  
 O **chave** objeto a ser acrescentado ou o nome da chave para criar e anexar.  
  
 *KeyType*  
 Opcional. Um **longo** valor que especifica o tipo de chave. O *chave* parâmetro corresponde do [tipo](../../../ado/reference/adox-api/type-property-key-adox.md) propriedade de um **chave** objeto.  
  
 *Coluna*  
 Opcional. Um **cadeia de caracteres** valor que especifica o nome da coluna a ser indexado. O *colunas* parâmetro corresponde ao valor da [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade de um [coluna](../../../ado/reference/adox-api/column-object-adox.md) objeto.  
  
 *RelatedTable*  
 Opcional. Um **cadeia de caracteres** valor que especifica o nome da tabela relacionada. O *RelatedTable* parâmetro corresponde ao valor da **nome** propriedade de um [tabela](../../../ado/reference/adox-api/table-object-adox.md) objeto.  
  
 *RelatedColumn*  
 Opcional. Um **cadeia de caracteres** valor que especifica o nome da coluna relacionada para uma chave estrangeira. O *RelatedColumn* parâmetro corresponde ao valor da **nome** propriedade de um [coluna](../../../ado/reference/adox-api/column-object-adox.md) objeto.  
  
## <a name="remarks"></a>Comentários  
 O *colunas* parâmetro pode ser o nome de uma coluna ou uma matriz de nomes de coluna.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo de propriedades de UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Acrescente o método (ADOX colunas)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [(Grupos de ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método (ADOX índices) append](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Acrescente o método (ADOX procedimentos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [(Tabelas ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Acrescente o método (ADOX usuários)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)

