---
description: Método Append (Chaves do ADOX)
title: Método Append (chaves ADOX) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ae3ef035594b696b829f0f1898e1749a2c33f11
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440528"
---
# <a name="append-method-adox-keys"></a>Método Append (Chaves do ADOX)
Adiciona um novo objeto de [chave](../../../ado/reference/adox-api/key-object-adox.md) à coleção de [chaves](../../../ado/reference/adox-api/keys-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Chave*  
 O objeto de **chave** a ser acrescentado ou o nome da chave a ser criada e acrescentada.  
  
 *KeyType*  
 Opcional. Um valor **longo** que especifica o tipo de chave. O parâmetro de *chave* corresponde à propriedade [Type](../../../ado/reference/adox-api/type-property-key-adox.md) de um objeto **Key** .  
  
 *Coluna*  
 Opcional. Um valor de **cadeia de caracteres** que especifica o nome da coluna a ser indexada. O parâmetro *Columns* corresponde ao valor da propriedade [Name](../../../ado/reference/adox-api/name-property-adox.md) de um objeto [Column](../../../ado/reference/adox-api/column-object-adox.md) .  
  
 *RelatedTable*  
 Opcional. Um valor de **cadeia de caracteres** que especifica o nome da tabela relacionada. O parâmetro *RELATEDTABLE* corresponde ao valor da propriedade **Name** de um objeto [Table](../../../ado/reference/adox-api/table-object-adox.md) .  
  
 *RelatedColumn*  
 Opcional. Um valor de **cadeia de caracteres** que especifica o nome da coluna relacionada para uma chave estrangeira. O parâmetro *RelatedColumn* corresponde ao valor da propriedade **Name** de um objeto [Column](../../../ado/reference/adox-api/column-object-adox.md) .  
  
## <a name="remarks"></a>Comentários  
 O parâmetro *Columns* pode ter o nome de uma coluna ou uma matriz de nomes de coluna.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Keys (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Método Append (colunas ADOX)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método Append (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Método Append (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Método Append (tabelas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
