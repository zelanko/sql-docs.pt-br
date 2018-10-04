---
title: Microsoft OLE DB Provider simples | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd22d13a0fe656a7d176d6fb9fd2a97e3ce8d3b0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673516"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Visão geral do Microsoft OLE DB Provider simples
O Microsoft OLE DB simples provedor OSP () permite que o ADO para acessar os dados para o qual um provedor tenha sido escrito usando o [Kit de ferramentas do OLE DB simples provedor (OSP)](http://msdn.microsoft.com/6e7b7931-9e4a-4151-ae51-672abd3f84a6). Provedores simples destinam-se para acessar fontes de dados que exigem suporte de OLE DB apenas fundamental, como matrizes na memória ou documentos XML.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para conectar o OLE DB simples DLL de provedor, defina as *provedor* argumento para o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```
MSDAOSP
```

 Esse valor também pode ser definido ou lidos usando o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade.

 Você pode conectar provedores simples que foram registrados como provedores de OLE DB completas usando o nome do provedor registrado, determinado pelo gravador do provedor.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de caracteres de conexão típica para esse provedor é:

```
"Provider=MSDAOSP;Data Source=serverName"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Description|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para SQL Server.|
|**Fonte de dados**|Especifica o nome de um servidor.|

## <a name="xml-document-example"></a>Exemplo de documento XML
 O OLE DB simples provedor OSP () no MDAC 2.7 ou posterior e Windows Data Access Components (Windows DAC) foi aprimorado para dar suporte à abertura ADO hierárquica **conjuntos de registros** sobre arquivos arbitrários de XML. Esses arquivos XML podem conter o esquema de persistência XML ADO, mas não é necessária. Isso foi implementado conectando-se a OSP para o **MSXML2.DLL**; portanto **MSXML2.DLL** ou posterior é necessário.

 O **Portfolio** arquivo usado no exemplo a seguir contém a árvore a seguir:

```
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 O DSO XML usa uma heurística interna para converter os nós em uma árvore XML em capítulos hierárquico **conjunto de registros**.

 Usando esse heurística interna, a árvore XML é convertida em um nível de dois hierárquico **Recordset** da seguinte forma:

```
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 Observe que as marcas de portfólio e informações não são representadas no hierárquica **conjunto de registros**. Para obter uma explicação de como o DSO XML converte árvores XML hierárquicos **conjuntos de registros**, consulte as regras a seguir. A coluna $Text é abordada na seção a seguir.

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>Regras para atribuição de elementos e atributos XML para colunas e linhas
 O DSO XML segue um procedimento para atribuição de elementos e atributos para colunas e linhas em aplicativos vinculados a dados. XML é modelado como uma árvore com uma marca que contém toda a hierarquia. Por exemplo, uma descrição XML de um livro pode conter marcas do capítulo, Figura marcas e marcas de seção. No nível mais alto, seria a marca do livro, que contém o capítulo subelementos, a figura e a seção. Quando o DSO XML mapeia os elementos XML em linhas e colunas, os subelementos, não o elemento de nível superior, são convertidos.

 O DSO XML usa este procedimento para converter os subelementos:

-   Cada atributo e um subelemento correspondem a uma coluna em algumas **Recordset** na hierarquia.

-   O nome da coluna é igual ao nome do subelemento ou atributo, a menos que o elemento pai tem um atributo e um subelemento com o mesmo nome, caso em que um "!" é anexado ao nome de coluna do subelemento.

-   Cada coluna é uma *simples* coluna que contém valores escalares (normalmente, cadeias de caracteres) ou um **conjunto de registros** coluna que contém o filho **conjuntos de registros**.

-   Colunas correspondentes aos atributos são sempre simples.

-   São colunas correspondentes a subelementos **Recordset** colunas se o subelemento possui seus próprio subelementos ou atributos (ou ambos), ou pai do subelemento tem mais de uma instância do subelemento como um filho. Caso contrário, a coluna é simple.

-   Quando houver várias instâncias de um subelemento (pais diferentes), uma coluna for um **conjunto de registros** coluna se *qualquer* das instâncias implica um **Recordset** coluna; sua coluna é simple somente se *todos os* instâncias implicam uma coluna simple.

-   Todos os **conjuntos de registros** têm uma coluna adicional chamada $Text.

 O código que é necessário para construir um **Recordset** é da seguinte maneira:

```
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "http://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  O caminho do arquivo de dados pode ser especificado usando quatro diferentes convenções de nomenclatura.

```
'HTTP://
adoRS.Open "http://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 Assim que o **conjunto de registros** tiver sido aberto, o ADO usual **Recordset** comandos de navegação podem ser usados.

 **Conjuntos de registros** gerados pela OSP têm algumas limitações:

-   Cursores do cliente (**adUseClient**) não têm suporte.

-   Hierárquica **conjuntos de registros** criados ao longo do arbitrário XML não pode ser persistente usando **Recordset.Save**.

-   **Conjuntos de registros** criado com a OSP são somente leitura.

-   O XMLDSO adiciona uma coluna adicional de dados ($Text) a cada **Recordset** na hierarquia.

 Para obter mais informações sobre o provedor OLE DB simples, consulte [criação de um provedor simples](http://msdn.microsoft.com/b31a6cba-58ae-4ee8-9039-700973d354d6).

## <a name="code-example"></a>Exemplo de código
 O código de Visual Basic a seguir demonstra abrindo um arquivo XML arbitrário, construindo um hierárquica **conjunto de registros**e recursivamente escrever cada registro de cada **Recordset** para a janela de depuração.

 Aqui está um arquivo XML simples que contém as cotações de ações. O código a seguir usa esse arquivo para construir um nível de dois hierárquico **conjunto de registros**.

```
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>http://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>http://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>http://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>http://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 A seguir estão as dois subprocedimentos do Visual Basic. O primeiro cria o **conjunto de registros** e passa-o para o *WalkHier* quais recursivamente conduz toda a hierarquia, escrever cada procedimento sub **campo** em cada registro em cada **Recordset** para a janela de depuração.

```
Private Sub BrowseHierRecordset()
' Add ADO 2.7 or later to Project/References
' No need to add MSXML2, ADO just passes the ProgID through to the OSP.

    Dim adoConn As ADODB.Connection
    Dim adoRS As ADODB.Recordset
    Dim adoChildRS As ADODB.Recordset

    Set adoConn = New ADODB.Connection
    Set adoRS = New ADODB.Recordset
    Set adoChildRS = ADODB.Recordset

    adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
    adoRS.Open "http://bwillett3/Kowalski/portfolio.xml", adoConn

    Dim iLevel As Integer
    iLevel = 0
    WalkHier iLevel, adoRS

End Sub

Sub WalkHier(ByVal iLevel As Integer, ByVal adoRS As ADODB.Recordset)
    iLevel = iLevel + 1
    PriorLevel = iLevel
    While Not adoRS.EOF
        For ndx = 0 To adoRS.Fields.Count - 1
            If adoRS.Fields(ndx).Name <> "$Text" Then
                If adoRS.Fields(ndx).Type = adChapter Then
                    Set adoChildRS = adoRS.Fields(ndx).Value
                    WalkHier iLevel, adoChildRS
                Else
                    Debug.Print iLevel & ": adoRS.Fields(" & ndx & _
                       ") = " & adoRS.Fields(ndx).Name & " = " & _
                       adoRS.Fields(ndx).Value
                End If
            End If
        Next ndx
        adoRS.MoveNext
    Wend
    iLevel = PriorLevel
End Sub
```
