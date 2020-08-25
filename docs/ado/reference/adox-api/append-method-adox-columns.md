---
description: Método Append (Colunas do ADOX)
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
ms.openlocfilehash: d17c6823acc945f50e5d8d0543448c997dadc5fe
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771515"
---
# <a name="append-method-adox-columns"></a>Método Append (Colunas do ADOX)
Adiciona um novo objeto de [coluna](./column-object-adox.md) à coleção de [colunas](./columns-collection-adox.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Coluna*  
 O objeto de **coluna** a ser anexado ou o nome da coluna a ser criada e acrescentada.  
  
 *Tipo*  
 Opcional. Um valor **longo** que especifica o tipo de dados da coluna. O parâmetro de *tipo* corresponde à propriedade [Type](./type-property-column-adox.md) de um objeto **Column** .  
  
 *DefinedSize*  
 Opcional. Um valor **longo** que especifica o tamanho da coluna. O parâmetro *DefinedSize* corresponde à propriedade [DefinedSize](./definedsize-property-adox.md) de um objeto **Column** .  
  
> [!NOTE]
>  Ocorrerá um erro ao acrescentar uma **coluna** à coleção de **colunas** de um [índice](./index-object-adox.md) se a **coluna** não existir em uma [tabela](./table-object-adox.md) que já esteja anexada à coleção de [tabelas](./tables-collection-adox.md) .  
  
## <a name="applies-to"></a>Aplica-se A  
 [Coleção Columns (ADOX)](./columns-collection-adox.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Método Append (grupos ADOX)](./append-method-adox-groups.md)   
 [Método Append (índices ADOX)](./append-method-adox-indexes.md)   
 [Método Append (chaves ADOX)](./append-method-adox-keys.md)   
 [Método Append (procedimentos do ADOX)](./append-method-adox-procedures.md)   
 [Método Append (tabelas ADOX)](./append-method-adox-tables.md)   
 [Método Append (usuários do ADOX)](./append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](./append-method-adox-views.md)