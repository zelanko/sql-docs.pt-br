---
description: Método Append (Chaves do ADOX)
title: Método Append (chaves ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 2531031808c16db4892fb0b759a8a8d819a2222d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985477"
---
# <a name="append-method-adox-keys"></a>Método Append (Chaves do ADOX)
Adiciona um novo objeto de [chave](./key-object-adox.md) à coleção de [chaves](./keys-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Keys.Append Key [,KeyType] [,Column] [,RelatedTable] [,RelatedColumn]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Chave*  
 O objeto de **chave** a ser acrescentado ou o nome da chave a ser criada e acrescentada.  
  
 *KeyType*  
 Opcional. Um valor **longo** que especifica o tipo de chave. O parâmetro de *chave* corresponde à propriedade [Type](./type-property-key-adox.md) de um objeto **Key** .  
  
 *Coluna*  
 Opcional. Um valor de **cadeia de caracteres** que especifica o nome da coluna a ser indexada. O parâmetro *Columns* corresponde ao valor da propriedade [Name](./name-property-adox.md) de um objeto [Column](./column-object-adox.md) .  
  
 *RelatedTable*  
 Opcional. Um valor de **cadeia de caracteres** que especifica o nome da tabela relacionada. O parâmetro *RELATEDTABLE* corresponde ao valor da propriedade **Name** de um objeto [Table](./table-object-adox.md) .  
  
 *RelatedColumn*  
 Opcional. Um valor de **cadeia de caracteres** que especifica o nome da coluna relacionada para uma chave estrangeira. O parâmetro *RelatedColumn* corresponde ao valor da propriedade **Name** de um objeto [Column](./column-object-adox.md) .  
  
## <a name="remarks"></a>Comentários  
 O parâmetro *Columns* pode ter o nome de uma coluna ou uma matriz de nomes de coluna.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Keys (ADOX)](./keys-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Método Append (colunas ADOX)](./append-method-adox-columns.md)   
 [Método Append (grupos ADOX)](./append-method-adox-groups.md)   
 [Método Append (índices ADOX)](./append-method-adox-indexes.md)   
 [Método Append (procedimentos do ADOX)](./append-method-adox-procedures.md)   
 [Método Append (tabelas ADOX)](./append-method-adox-tables.md)   
 [Método Append (usuários do ADOX)](./append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](./append-method-adox-views.md)