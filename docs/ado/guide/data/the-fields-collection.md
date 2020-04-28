---
title: A coleção Fields | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 197a57b8a9b9ea2927a057733992a02c731a335a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923935"
---
# <a name="the-fields-collection"></a>A coleção Field
A coleção **Fields** é uma das coleções intrínsecas do ADO. Uma coleção é um conjunto ordenado de itens que podem ser referidos como uma unidade. Para obter mais informações sobre coleções ADO, consulte [o modelo de objeto ADO](../../../ado/guide/data/ado-objects-and-collections.md).  
  
 A coleção **Fields** contém um objeto **Field** para cada campo (coluna) no **conjunto de registros**. Como todas as coleções ADO, ele tem propriedades **Count** e **Item** , bem como métodos **Append** e **Refresh** . Ele também tem os métodos **CancelUpdate**, **delete**, **Ressync**e **Update** , que não estão disponíveis para outras coleções do ADO.  
  
## <a name="examining-the-fields-collection"></a>Examinando a coleção Fields  
 Considere a coleção **Fields** do **conjunto de registros** de exemplo introduzido nesta seção. O **conjunto de registros** de exemplo foi derivado da instrução SQL  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 Portanto, você deve descobrir que a coleção de **campos do conjunto de registros** contém três campos.  
  
```  
'BeginWalkFields  
    Dim objFields As ADODB.Fields  
    Dim intLoop As Integer  
  
    objRs.Open strSQL, strConnStr, adOpenForwardOnly, adLockReadOnly, adCmdText  
  
    Set objFields = objRs.Fields  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
    Next  
'EndWalkFields  
```  
  
 Esse código simplesmente determina o número de objetos **Field** na coleção **Fields** usando a propriedade **Count** e faz um loop pela coleção, retornando o valor da propriedade **Name** para cada objeto **Field** . Você pode usar muito mais propriedades de **campo** para obter informações sobre um campo. Para obter mais informações sobre como consultar um **campo**, consulte [o objeto Field](../../../ado/guide/data/the-field-object.md).  
  
## <a name="counting-columns"></a>Colunas de contagem  
 Como você deve esperar, a propriedade **Count** retorna o número real de objetos **Field** na coleção **Fields** . Como a numeração de membros de uma coleção começa com zero, você deve sempre codificar loops começando com o membro zero e terminando com o valor da propriedade **Count** menos 1. Se você estiver usando o Microsoft Visual Basic e quiser executar um loop pelos membros de uma coleção sem verificar a propriedade **Count** , use o **para cada... Próximo** comando.  
  
 Se a propriedade **Count** for zero, não haverá nenhum objeto na coleção.  
  
## <a name="getting-to-the-field"></a>Chegar ao campo  
 Assim como ocorre com qualquer coleção ADO, a propriedade **Item** é a propriedade padrão da coleção. Ele retorna o objeto de **campo** individual especificado pelo nome ou índice passado para ele. Portanto, as instruções a seguir são equivalentes ao **conjunto de registros**de exemplo:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 Se esses métodos são equivalentes, o que é melhor? Isso depende. Usar um índice para recuperar um **campo** da coleção é mais rápido porque acessa o **campo** diretamente sem precisar executar uma pesquisa de cadeia de caracteres. Por outro lado, a ordem dos **campos** na coleção deve ser conhecida e, se a ordem for alterada, a referência ao índice **do campo** terá que ser alterada onde quer que ocorra. Embora um pouco mais lento, o uso do nome do **campo** é mais flexível porque não depende da ordem dos **campos** na coleção.  
  
## <a name="using-the-refresh-method"></a>Usando o método Refresh  
 Ao contrário de algumas outras coleções do ADO, o uso do método **Refresh** na coleção **Fields** não tem efeito visível. Para recuperar as alterações da estrutura de banco de dados subjacente, você deve usar o método **Requery** ou se o objeto **Recordset** não oferecer suporte a indicadores, o método **MoveFirst** , que fará com que o comando seja executado no provedor novamente.  
  
## <a name="adding-fields-to-a-recordset"></a>Adicionando campos a um conjunto de registros  
 O método **Append** é usado para adicionar campos a um **conjunto de registros**.  
  
 Você pode usar o método **Append** para malhar um **conjunto de registros** programaticamente sem abrir uma conexão com uma fonte de dados. Ocorrerá um erro em tempo de execução se o método **Append** for chamado na coleção **Fields** de um **conjunto de registros** aberto ou em um conjunto de **registros** em que a propriedade **ActiveConnection** foi definida. Você pode acrescentar campos somente a um **conjunto de registros** que não esteja aberto e que ainda não tenha sido conectado a uma fonte de dados. No entanto, para especificar valores para os **campos**acrescentados recentemente, o **conjunto de registros** deve ser aberto primeiro.  
  
 Os desenvolvedores geralmente precisam de um local para armazenar temporariamente alguns dados ou querem que alguns dados atuem como se esvenhassem de um servidor para que possam participar da ligação de dados em uma interface do usuário. O ADO (em conjunto com o [serviço de cursor da Microsoft para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) permite que o desenvolvedor crie um objeto **Recordset** vazio especificando informações de coluna e chamando **Open**. No exemplo a seguir, três novos campos são anexados a um novo objeto **Recordset** . Em seguida, o **conjunto de registros** é aberto, dois novos registros são adicionados e o **conjunto de registros** é persistido em um arquivo. (Para obter mais informações sobre persistência de **conjunto de registros** , consulte [atualizando e mantendo dados](../../../ado/guide/data/updating-and-persisting-data.md).)  
  
```  
'BeginFabricate  
    Dim objRs As ADODB.Recordset  
    Set objRs = New ADODB.Recordset  
  
    With objRs.Fields  
        .Append "StudentID", adChar, 11, adFldUpdatable  
        .Append "FullName", adVarChar, 50, adFldUpdatable  
        .Append "PhoneNmbr", adVarChar, 20, adFldUpdatable  
    End With  
  
    With objRs  
        .Open  
  
        .AddNew  
        .Fields(0) = "123-45-6789"  
        .Fields(1) = "John Doe"  
        .Fields(2) = "(425) 555-5555"  
        .Update  
  
        .AddNew  
        .Fields(0) = "123-45-6780"  
        .Fields(1) = "Jane Doe"  
        .Fields(2) = "(615) 555-1212"  
        .Update  
    End With  
  
    objRs.Save App.Path & "FabriTest.adtg", adPersistADTG  
  
    objRs.Close  
'EndFabricate  
```  
  
 O uso do método **Append de campos** difere entre o objeto **Recordset** e o objeto **Record** . Para obter mais informações sobre o objeto **Record** , consulte [registros e fluxos](../../../ado/guide/data/records-and-streams.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Fabricar conjuntos de registros hierárquicos](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)
