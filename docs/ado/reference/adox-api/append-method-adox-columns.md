---
title: Método Append (colunas ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e69f2510e825a935cf7eb34951051c1e3848bb9
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764037"
---
# <a name="append-method-adox-columns"></a>Método Append (Colunas do ADOX)
Adiciona um novo objeto de [coluna](../../../ado/reference/adox-api/column-object-adox.md) à coleção de [colunas](../../../ado/reference/adox-api/columns-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Coluna*  
 O objeto de **coluna** a ser anexado ou o nome da coluna a ser criada e acrescentada.  
  
 *Tipo*  
 Opcional. Um valor **longo** que especifica o tipo de dados da coluna. O parâmetro de *tipo* corresponde à propriedade [Type](../../../ado/reference/adox-api/type-property-column-adox.md) de um objeto **Column** .  
  
 *DefinedSize*  
 Opcional. Um valor **longo** que especifica o tamanho da coluna. O parâmetro *DefinedSize* corresponde à propriedade [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) de um objeto **Column** .  
  
> [!NOTE]
>  Ocorrerá um erro ao acrescentar uma **coluna** à coleção de **colunas** de um [índice](../../../ado/reference/adox-api/index-object-adox.md) se a **coluna** não existir em uma [tabela](../../../ado/reference/adox-api/table-object-adox.md) que já esteja anexada à coleção de [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Método Append (grupos ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método Append (índices ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Método Append (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Método Append (tabelas ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Método Append (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
