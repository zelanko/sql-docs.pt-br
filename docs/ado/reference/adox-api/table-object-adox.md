---
description: Objeto Table (ADOX)
title: Objeto Table (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
author: rothja
ms.author: jroth
ms.openlocfilehash: 847918f13dd6c91a707e660e97d1dbc4de499442
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769295"
---
# <a name="table-object-adox"></a>Objeto Table (ADOX)
Representa uma tabela de banco de dados, incluindo colunas, índices e chaves.  
  
## <a name="remarks"></a>Comentários  
 O código a seguir cria uma nova **tabela**:  
  
```  
Dim obj As New Table  
```  
  
 Com as propriedades e coleções de um objeto **Table** , você pode:  
  
-   Identifique a tabela com a propriedade [Name (ADOX)](./name-property-adox.md) .  
  
-   Determine o tipo de tabela com a propriedade ( [tabela) do tipo Propriedade (ADOX)](./type-property-table-adox.md) .  
  
-   Acesse as colunas de banco de dados da tabela com a coleção de [colunas (ADOX)](./columns-collection-adox.md) .  
  
-   Acesse os índices da tabela com a [coleção de índices (ADOX)](./indexes-collection-adox.md).  
  
-   Acesse as chaves da tabela com a [coleção de chaves (ADOX)](./keys-collection-adox.md).  
  
-   Especifique o catálogo que possui a tabela com a propriedade [ParentCatalog (ADOX)](./parentcatalog-property-adox.md) .  
  
-   Retornar informações de data com as propriedades da propriedade [DateCreated (ADOX)](./datecreated-property-adox.md) e da [Propriedade DateModified (ADOX)](./datemodified-property-adox.md) .  
  
-   Acesse Propriedades de tabela específicas do provedor com a coleção de [Propriedades Collection (ADO)](../ado-api/properties-collection-ado.md) .  
  
> [!NOTE]
>  Seu provedor de dados pode não dar suporte a todas as propriedades de objetos de **tabela** . Ocorrerá um erro se você tiver definido um valor para uma propriedade para a qual o provedor não oferece suporte. Para novos objetos **Table** , o erro ocorrerá quando o objeto for anexado à coleção. Para objetos existentes, o erro ocorrerá ao definir a propriedade.  
>   
>  Ao criar objetos de **tabela** , a existência de um valor padrão apropriado para uma propriedade opcional não garante que seu provedor dê suporte à propriedade. Para obter mais informações sobre quais propriedades seu provedor dá suporte, consulte a documentação do provedor.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, Métodos e Eventos do objeto Table](./table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade ActiveConnection do catálogo (VB)](./catalog-activeconnection-property-example-vb.md)   
 [Exemplo da propriedade Name e métodos de acréscimo de colunas e tabelas (VB)](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Método Connection Close, exemplo da propriedade de tipo Table (VB)](./connection-close-method-table-type-property-example-vb.md)   
 [Exemplo das propriedades método, tipo de chave, RelatedColumn, RELATEDTABLE e UpdateRule da tecla Append (VB)](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Exemplo da propriedade ParentCatalog (VB)](./parentcatalog-property-example-vb.md)   
 [Coleção Columns (ADOX)](./columns-collection-adox.md)   
 [Coleção de índices (ADOX)](./indexes-collection-adox.md)   
 [Coleção Keys (ADOX)](./keys-collection-adox.md)   
 [Coleção Properties (ADO)](../ado-api/properties-collection-ado.md)   
 [Coleção Tables (ADOX)](./tables-collection-adox.md)