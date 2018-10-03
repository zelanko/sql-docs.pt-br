---
title: (Colunas do ADOX) do método append | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 98ff605c2fb701f2451e3df4ba2068da6729ff86
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47845284"
---
# <a name="append-method-adox-columns"></a>Método Append (Colunas do ADOX)
Adiciona um novo [coluna](../../../ado/reference/adox-api/column-object-adox.md) do objeto para o [colunas](../../../ado/reference/adox-api/columns-collection-adox.md) coleção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Columns.Append Column [,Type] [,DefinedSize]  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Coluna*  
 O **coluna** objeto a ser acrescentado ou o nome da coluna para criar e anexar.  
  
 *Tipo*  
 Opcional. Um **longo** valor que especifica o tipo de dados da coluna. O *tipo* parâmetro corresponde à [tipo](../../../ado/reference/adox-api/type-property-column-adox.md) propriedade de um **coluna** objeto.  
  
 *DefinedSize*  
 Opcional. Um **longo** valor que especifica o tamanho da coluna. O *DefinedSize* parâmetro corresponde à [DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md) propriedade de um **coluna** objeto.  
  
> [!NOTE]
>  Ocorrerá um erro ao anexar um **coluna** para o **colunas** coleção de um [índice](../../../ado/reference/adox-api/index-object-adox.md) se o **coluna** não existe em um [Tabela](../../../ado/reference/adox-api/table-object-adox.md) que já é acrescentado para o [tabelas](../../../ado/reference/adox-api/tables-collection-adox.md) coleção.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Coleção Columns (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)  
  
## <a name="see-also"></a>Consulte também  
 [Columns and Tables Append métodos, exemplo da propriedade Name (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Chaves de acrescentar o método, tipo de chave, RelatedColumn, RelatedTable e exemplo das propriedades UpdateRule (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Acrescentar o método (grupos do ADOX)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Acrescentar o método (índices do ADOX)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Acrescentar o método (chaves do ADOX)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Acrescentar o método (procedimentos do ADOX)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Acrescentar o método (tabelas do ADOX)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Acrescentar o método (usuários do ADOX)](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Método Append (Exibições do ADOX)](../../../ado/reference/adox-api/append-method-adox-views.md)
