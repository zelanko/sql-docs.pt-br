---
title: Acessando linhas em um conjunto de registros hierárquico | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83b8334b4891d0b12cac59030ebf7fced871c5dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773374"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>Acessando linhas em um conjunto de registros hierárquico (exemplo)
O exemplo a seguir mostra as etapas necessárias para linhas de acesso em modo hierárquico [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **Conjunto de registros** objetos de **autores** e **titleauthor** tabelas estão relacionadas pelo ID do autor.

2.  O loop externo exibe o nome e sobrenome, estado e identificação de cada autor.

3.  O acréscimo **conjunto de registros** para cada linha é recuperada do [campos](../../../ado/reference/ado-api/fields-collection-ado.md) coleção e atribuído à *rstTitleAuthor*.

4.  O loop interno exibe quatro campos de cada linha no acréscimo **conjunto de registros**.

 O [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) estiver definida como **falso** para fins de ilustração, para que você possa ver o capítulo alterar explicitamente em cada iteração do loop externo. Para tornar o exemplo de código mais eficiente, você pode mover a atribuição na etapa 3, antes da primeira linha na etapa 2, para que a atribuição seja executada apenas uma vez. Em seguida, defina a [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) propriedade **verdadeiro**, de modo que *rstTitleAuthor* implicitamente e automaticamente alterará o capítulo correspondente sempre que *rst* move para uma nova linha.

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
 [Visão geral de modelagem de dados](../../../ado/guide/data/data-shaping-overview.md) [objeto Field](../../../ado/reference/ado-api/field-object.md) [(ADO) da coleção de campos](../../../ado/reference/ado-api/fields-collection-ado.md) [gramática de forma Formal](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft Data Shaping Service para OLE DB (Provedor de serviços do ADO) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [necessários provedores para Data Shaping](../../../ado/guide/data/required-providers-for-data-shaping.md) [cláusula APPEND de forma](../../../ado/guide/data/shape-append-clause.md) [comandos da forma Gerais](../../../ado/guide/data/shape-commands-in-general.md) [cláusula COMPUTE de forma](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic para funções de aplicativos](../../../ado/guide/data/visual-basic-for-applications-functions.md)
