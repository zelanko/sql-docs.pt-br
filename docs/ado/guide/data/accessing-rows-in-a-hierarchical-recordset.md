---
title: Acessar linhas em um conjunto de registros hierárquico | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e7767fdbd933884116c77a67d1930171edf8a878
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>Acessar linhas em um conjunto de registros hierárquico (exemplo)
O exemplo a seguir mostra as etapas necessárias para acesso de linhas em um hierárquica [registros](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **Conjunto de registros** de objetos a partir de **autores** e **titleauthor** tabelas são relacionadas pela ID do autor.

2.  O loop externo exibe o nome e sobrenome de cada autor, estado e identificação.

3.  O acrescentados **registros** para cada linha é recuperada do [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleta e atribuído a *rstTitleAuthor*.

4.  O loop interno exibe quatro campos de cada linha o acrescentados **registros**.

 O [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) está definida como **false** para fins de ilustração, para que você possa ver o capítulo alterar explicitamente em cada iteração do loop externo. Para tornar o exemplo de código mais eficiente, você pode mover a atribuição na etapa 3 antes da primeira linha na etapa 2, para que a atribuição é executada apenas uma vez. Em seguida, defina o [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) propriedade **true**, de modo que *rstTitleAuthor* implicitamente e automaticamente alterará o capítulo correspondente sempre que *primeira* move para uma nova linha.

## <a name="example"></a>Exemplo

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## <a name="see-also"></a>Consulte também
 [Visão geral de modelagem de dados](../../../ado/guide/data/data-shaping-overview.md) [campo objeto](../../../ado/reference/ado-api/field-object.md) [(ADO) da coleção de campos](../../../ado/reference/ado-api/fields-collection-ado.md) [Formal de forma gramática](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft Data Shaping Service para OLE DB (Provedor de serviços de ADO) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [o objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [necessário provedores para modelagem de dados](../../../ado/guide/data/required-providers-for-data-shaping.md) [cláusula APPEND de forma](../../../ado/guide/data/shape-append-clause.md) [comandos de forma Geral](../../../ado/guide/data/shape-commands-in-general.md) [cláusula de computação de forma](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic para funções de aplicativos](../../../ado/guide/data/visual-basic-for-applications-functions.md)
