---
title: "A coleção de campos | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2c5d81985322b03892d17875959086078defd819
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="the-fields-collection"></a>A coleção de campos
O **campos** coleção é uma das coleções intrínsecas do ADO. Uma coleção é um conjunto ordenado de itens que podem ser referenciados como uma unidade. Para obter mais informações sobre coleções de ADO, consulte [o modelo de objeto ADO](../../../ado/guide/data/ado-objects-and-collections.md).  
  
 O **campos** coleção contém um **campo** objeto para cada campo (coluna) a **registros**. Como todas as coleções de ADO, ele tem **contagem** e **Item** propriedades, bem como **Append** e **atualização** métodos. Ele também tem **CancelUpdate**, **excluir**, **Resync**, e **atualização** métodos, que não estão disponíveis para outras coleções do ADO.  
  
## <a name="examining-the-fields-collection"></a>Examinando a coleção de campos  
 Considere o **campos** coleção do exemplo **registros** apresentados nesta seção. O exemplo **registros** foi derivada da instrução SQL  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 Portanto, você deve considerar que o **Recordset Fields** coleção contém três campos.  
  
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
  
 Esse código simplesmente determina o número de **campo** objetos no **campos** coleção usando o **contagem** propriedade e loops por meio da coleção, retornar o valor de o **nome** propriedade para cada **campo** objeto. Você pode usar muitas outras **campo** propriedades para obter informações sobre um campo. Para obter mais informações sobre como consultar um **campo**, consulte [o objeto de campo](../../../ado/guide/data/the-field-object.md).  
  
## <a name="counting-columns"></a>Contagem de colunas  
 Como esperado, o **contagem** propriedade retorna o número real de **campo** objetos no **campos** coleção. Como a numeração de membros de uma coleção começa com zero, você sempre deve codificar loops iniciando com zero membro e terminando com o valor da **contagem** propriedade menos 1. Se você estiver usando o Microsoft Visual Basic e deseja executar um loop através dos membros de uma coleção sem verificar o **contagem** propriedade, use o **para cada um... Próxima** comando.  
  
 Se o **contagem** é zero, não existem objetos na coleção.  
  
## <a name="getting-to-the-field"></a>Obtendo o campo  
 Assim como acontece com qualquer coleção de ADO, o **Item** propriedade é a propriedade padrão da coleção. Retorna o indivíduo **campo** o objeto especificado pelo nome ou índice passados para ele. Portanto, as instruções a seguir são equivalentes para o exemplo **registros**:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 Se esses métodos são equivalentes, que é melhor? Ele depende. Usando um índice para recuperar um **campo** da coleção é mais rápido porque ela acessa o **campo** diretamente sem a necessidade de executar uma pesquisa de cadeia de caracteres. Por outro lado, a ordem de **campos** dentro da coleção deve ser conhecida, e se a ordem de alterações, a referência para o **do campo** índice precisa ser alterada sempre que ela ocorre. Embora um pouco mais lentas, usando o nome do **campo** é mais flexível porque ele não depende na ordem do **campos** na coleção.  
  
## <a name="using-the-refresh-method"></a>Usando o método de atualização  
 Ao contrário de algumas outras coleções de ADO, usando o **atualizar** método o **campos** coleção não tem nenhum efeito visível. Para recuperar as alterações da estrutura de banco de dados subjacente, você deve usar o **Requery** método, ou se o **registros** objeto não oferece suporte a indicadores, o **MoveFirst**método, o que fará com que o comando a ser executado novamente em relação ao provedor.  
  
## <a name="adding-fields-to-a-recordset"></a>Adicionar campos a um conjunto de registros  
 O **Append** método é usado para adicionar campos a uma **registros**.  
  
 Você pode usar o **Append** método para fabricar um **registros** programaticamente sem abrir uma conexão com uma fonte de dados. Ocorrerá um erro de tempo de execução se o **acrescentar** método é chamado no **campos** coleção de um aberto **registros** ou em um **Recordset** onde o **ActiveConnection** propriedade foi definida. Você pode acrescentar campos apenas a um **registros** que não está aberto e ainda não foi conectado a uma fonte de dados. No entanto, para especificar valores para recentemente adicionada **campos**, o **registros** primeiro deve ser aberta.  
  
 Geralmente, os desenvolvedores precisam um lugar para armazenar alguns dados temporariamente ou deseja que alguns dados para atuar como se ela foi originada de um servidor para que ele possa participar de associação de dados em uma interface do usuário. ADO (em conjunto com o [do serviço Microsoft Cursor do OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)) permite que o desenvolvedor crie vazio **registros** objeto especificando informações de coluna e chamar **abrir**. No exemplo a seguir, três novos campos são anexados a um novo **registros** objeto. O **registros** é aberto, dois novos registros são adicionados e o **registros** é mantido em um arquivo. (Para obter mais informações sobre **registros** persistência, consulte [atualizando e dados persistentes](../../../ado/guide/data/updating-and-persisting-data.md).)  
  
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
  
 O uso do **acrescentar campos** método difere entre o **registros** objeto e o **registro** objeto. Para obter mais informações sobre o **registro** de objeto, consulte [registros e fluxos](../../../ado/guide/data/records-and-streams.md).  
  
## <a name="see-also"></a>Consulte também  
 [Fabricando conjuntos de registros hierárquicos](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)

