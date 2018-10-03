---
title: A coleção de campos | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 4bd852423ed285165b4d699b391807b9a748f9b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47730667"
---
# <a name="the-fields-collection"></a>A coleção Field
O **campos** coleção é uma das coleções de intrínsecos do ADO. Uma coleção é um conjunto ordenado de itens que podem ser referenciados como uma unidade. Para obter mais informações sobre coleções ADO, consulte [o modelo de objeto ADO](../../../ado/guide/data/ado-objects-and-collections.md).  
  
 O **campos** coleção contém um **campo** do objeto para cada campo (coluna) na **conjunto de registros**. Como todas as coleções do ADO, ele tem **contagem** e **Item** as propriedades, bem como **Append** e **atualizar** métodos. Ele também tem **CancelUpdate**, **excluir**, **ressincronizar**, e **atualização** métodos, que não estão disponíveis para outras coleções do ADO.  
  
## <a name="examining-the-fields-collection"></a>Examinando a coleção de campos  
 Considere a **campos** coleção da amostra **Recordset** apresentadas nesta seção. O exemplo **Recordset** foi derivado da instrução SQL  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 Portanto, você deverá notar que o **Recordset Fields** coleção contém três campos.  
  
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
  
 Esse código simplesmente determina o número de **campo** objetos na **campos** coleção usando o **contagem** propriedade e loops por meio da coleção, retornando o valor de o **nome** propriedade para cada **campo** objeto. Você pode usar muitas outras **campo** propriedades para obter informações sobre um campo. Para obter mais informações sobre como consultar um **campo**, consulte [o objeto de campo](../../../ado/guide/data/the-field-object.md).  
  
## <a name="counting-columns"></a>Contagem de colunas  
 Como você pode esperar, o **contagem** propriedade retorna o número real de **campo** objetos no **campos** coleção. Como a numeração de membros de uma coleção começa com zero, você deve sempre codificar loops começando com o membro zero e terminando com o valor da **contagem** propriedade menos 1. Se você estiver usando o Microsoft Visual Basic e deseja executar um loop através dos membros de uma coleção sem verificar a **contagem** propriedade, use o **para cada um... Próxima** comando.  
  
 Se o **contagem** for zero, não existem objetos na coleção.  
  
## <a name="getting-to-the-field"></a>Introdução ao campo  
 Assim como acontece com qualquer coleção de ADO, o **Item** propriedade é a propriedade padrão da coleção. Ele retorna o indivíduo **campo** objeto especificado pelo nome ou índice passado para ele. Portanto, as instruções a seguir são equivalentes para o exemplo **Recordset**:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 Se esses métodos são equivalentes, que é melhor? Ele depende. Usando um índice para recuperar um **campo** da coleção é mais rápido porque ela acessa o **campo** diretamente sem ter que executar uma pesquisa de cadeia de caracteres. Por outro lado, a ordem dos **campos** dentro da coleção deve ser conhecido, e se a ordem é alterada, a referência para o **do campo** índice precisará ser alterado sempre que ele ocorre. Embora um pouco mais lento, usando o nome da **campo** é mais flexível porque ele não depende na ordem dos **campos** na coleção.  
  
## <a name="using-the-refresh-method"></a>Usando o método de atualização  
 Ao contrário de algumas outras coleções de ADO, usando o **Refresh** método na **campos** coleção não tem nenhum efeito visível. Para recuperar as alterações da estrutura de banco de dados subjacente, você deve usar o **Requery** método, ou se o **conjunto de registros** objeto não oferece suporte a indicadores, o **MoveFirst**método, o que fará com que o comando para ser executada novamente no provedor.  
  
## <a name="adding-fields-to-a-recordset"></a>Adicionar campos a um conjunto de registros  
 O **Append** método é usado para adicionar campos para um **conjunto de registros**.  
  
 Você pode usar o **Append** método para fabricar um **Recordset** programaticamente sem abrir uma conexão a uma fonte de dados. Um erro de tempo de execução ocorrerá se o **Append** método é chamado na **campos** coleção de um aberto **conjunto de registros** ou em um **Recordset** em que o **ActiveConnection** propriedade foi definida. Você pode acrescentar campos apenas a um **Recordset** que não está aberto e ainda não foi conectado a uma fonte de dados. No entanto, para especificar valores para recentemente adicionada à **campos**, o **Recordset** deve primeiro ser aberto.  
  
 Os desenvolvedores geralmente precisam de um lugar para armazenar alguns dados temporariamente ou desejar que alguns dados aja como se ela veio de um servidor para que ele possa participar de associação de dados em uma interface do usuário. ADO (em conjunto com o [Microsoft Cursor Service para OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) permite que o desenvolvedor criar vazio **conjunto de registros** objeto especificando informações de coluna e chamar **abrir**. No exemplo a seguir, três novos campos são anexados a uma nova **Recordset** objeto. Em seguida, a **conjunto de registros** é aberto, dois novos registros são adicionados e o **Recordset** é mantido em um arquivo. (Para obter mais informações sobre **conjunto de registros** persistência, consulte [atualizando e persistência de dados](../../../ado/guide/data/updating-and-persisting-data.md).)  
  
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
  
 O uso do **campos de acréscimo** método difere entre o **conjunto de registros** objeto e o **registro** objeto. Para obter mais informações sobre o **registro** do objeto, consulte [registros e fluxos](../../../ado/guide/data/records-and-streams.md).  
  
## <a name="see-also"></a>Consulte também  
 [Fabricando conjuntos de registros hierárquicos](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)
