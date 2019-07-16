---
title: Método (chaves do ADOX) append | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Keys::Append
- Keys::raw_Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 215a5391-f422-42ec-99ea-4e6fbb5d3d64
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd66edb75bec4f4b7e35c53c9ebeabd9b3c75d83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67967294"
---
# <a name="append-method-adox-keys"></a>Método Append (Chaves do ADOX)
Adiciona um novo [chave](../../../ado/reference/adox-api/key-object-adox.md) do objeto para o [chaves](../../../ado/reference/adox-api/keys-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Chave*  
 O **chave** objeto a ser acrescentado ou o nome da chave para criar e anexar.  
  
 *KeyType*  
 Opcional. Um **longo** valor que especifica o tipo de chave. O *chave* parâmetro corresponde à [tipo](../../../ado/reference/adox-api/type-property-key-adox.md) propriedade de um **chave** objeto.  
  
 *Coluna*  
 Opcional. Um **cadeia de caracteres** valor que especifica o nome da coluna a ser indexado. O *colunas* parâmetro corresponde ao valor da [nome](../../../ado/reference/adox-api/name-property-adox.md) propriedade de um [coluna](../../../ado/reference/adox-api/column-object-adox.md) objeto.  
  
 *RelatedTable*  
 Opcional. Um **cadeia de caracteres** valor que especifica o nome da tabela relacionada. O *RelatedTable* parâmetro corresponde ao valor da **nome** propriedade de um [tabela](../../../ado/reference/adox-api/table-object-adox.md) objeto.  
  
 *RelatedColumn*  
 Opcional. Um **cadeia de caracteres** valor que especifica o nome da coluna relacionada para uma chave estrangeira. O *RelatedColumn* parâmetro corresponde ao valor da **nome** propriedade de um [coluna](../../../ado/reference/adox-api/column-object-adox.md) objeto.  
  
## <a name="remarks"></a>Comentários  
 O *colunas* parâmetro pode assumir o nome de uma coluna ou uma matriz de nomes de coluna.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo das propriedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Acrescentar o método (colunas do ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Acrescentar o método (grupos do ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Acrescentar o método (índices do ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Acrescentar o método (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Acrescentar o método (tabelas do ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Acrescentar o método (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
