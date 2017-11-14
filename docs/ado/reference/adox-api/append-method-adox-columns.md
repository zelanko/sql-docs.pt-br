---
title: "Método (ADOX colunas) append | Microsoft Docs"
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
- Columns::raw_Append
- Columns::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 7a46d23c-efef-4ec7-815d-cd3ac86787dd
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7c6c9323dbc1e3c69445dc09ad06373856fb67bc
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-columns"></a>Acrescente o método (ADOX colunas)
Adiciona um novo [coluna](../../../ado/reference/adox-api/column-object-adox.md) o objeto para o [colunas](../../../ado/reference/adox-api/columns-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Coluna*  
 O **coluna** objeto a ser acrescentado ou o nome da coluna para criar e anexar.  
  
 *Tipo*  
 Opcional. Um **longo** valor que especifica o tipo de dados da coluna. O *tipo* parâmetro corresponde do [tipo](../../../ado/reference/adox-api/type-property-column-adox.md) propriedade de um **coluna** objeto.  
  
 *DefinedSize*  
 Opcional. Um **longo** valor que especifica o tamanho da coluna. O *DefinedSize* parâmetro corresponde do [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) propriedade de um **coluna** objeto.  
  
> [!NOTE]
>  Ocorrerá um erro ao anexar um **coluna** para o **colunas** coleção de um [índice](../../../ado/reference/adox-api/index-object-adox.md) se o **coluna** não existe em um [Tabela](../../../ado/reference/adox-api/table-object-adox.md) que já está anexado ao [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) coleção.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e colunas acrescentar métodos, exemplo de nome de propriedade (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo de propriedades de UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo de propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [(Grupos de ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Método (ADOX índices) append](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [(ADOX chaves) do método append](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescente o método (ADOX procedimentos)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [(Tabelas ADOX) do método append](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Acrescente o método (ADOX usuários)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)

