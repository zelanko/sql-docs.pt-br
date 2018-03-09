---
title: Microsoft OLE DB Provider simples | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ae0672fc209e2a31608a36fdef6757bef8d60cf6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Visão geral do Microsoft OLE DB Provider simples
O Microsoft OLE DB simples provedor (OSP) permite que o ADO acessar os dados para o qual um provedor foi criado com o [Kit de ferramentas do OLE DB simples provedor (OSP)](http://msdn.microsoft.com/en-us/6e7b7931-9e4a-4151-ae51-672abd3f84a6). Provedores simples destinam-se para acessar fontes de dados que exigem suporte de OLE DB apenas fundamental, como matrizes de memória ou documentos XML.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de caracteres de Conexão
 Para conectar o OLE DB simples DLL de provedor, defina o *provedor* argumento para o [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade para:

```
MSDAOSP
```

 Esse valor também pode ser definido ou lidos usando o [provedor](../../../ado/reference/ado-api/provider-property-ado.md) propriedade.

 Você pode se conectar a provedores simples que foram registrados como provedores de OLE DB completas usando o nome de provedor registrado, determinado pelo gerador de provedor.

## <a name="typical-connection-string"></a>Cadeia de caracteres de Conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```
"Provider=MSDAOSP;Data Source=serverName"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Description|
|-------------|-----------------|
|**Provedor**|Especifica o provedor OLE DB para SQL Server.|
|**Fonte de dados**|Especifica o nome de um servidor.|

## <a name="xml-document-example"></a>Exemplo de documento XML
 O OLE DB simples provedor (OSP) no MDAC 2.7 ou posterior e Windows Data Access Components (Windows DAC) foi aprimorado para oferecer suporte à abertura ADO hierárquica **conjuntos de registros** em relação aos arquivos XML arbitrários. Esses arquivos XML podem conter o esquema de persistência XML ADO, mas não é necessário. Isso foi implementado por meio da conexão OSP para o **MSXML2.DLL**; portanto **Msxml2. dll** ou posterior é necessário.

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

 O DSO XML usa heurística interna para converter os nós em uma árvore XML em capítulos hierárquico **registros**.

 Usando essas heurística interna, a árvore XML é convertida em um nível de dois hierárquico **registros** da seguinte forma:

```
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 Observe que as marcas de portfólio e informações não são representadas no hierárquica **registros**. Para obter uma explicação de como o DSO XML converte árvores XML hierárquica **conjuntos de registros**, consulte as seguintes regras. A coluna $Text é abordada na seção a seguir.

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>Regras de atribuição de elementos e atributos XML para colunas e linhas
 O DSO XML segue um procedimento para atribuição de elementos e atributos para colunas e linhas em aplicativos de associação de dados. XML é modelado como uma árvore com uma marca que contém toda a hierarquia. Por exemplo, uma descrição XML de um livro pode conter marcas de capítulo, Figura marcas e marcas de seção. O nível mais alto seria a marca de catálogo, que contém o capítulo subelementos, a figura e a seção. Quando o DSO XML mapear elementos XML para linhas e colunas, os subelementos, não o elemento de nível superior, são convertidos.

 O DSO XML usa este procedimento para converter os subelementos:

-   Cada atributo e um subelemento correspondem a uma coluna em algumas **registros** na hierarquia.

-   O nome da coluna é o mesmo que o nome do atributo ou subelemento, a menos que o elemento pai tem um atributo e um subelemento com o mesmo nome, caso em que um "!" é anexado ao nome de coluna do subelemento.

-   Cada coluna é uma *simples* coluna que contém valores escalares (normalmente cadeias de caracteres) ou um **registros** coluna que contém o filho **conjuntos de registros**.

-   Colunas correspondentes aos atributos são sempre simples.

-   Colunas correspondentes subelementos são **registros** colunas se o subelemento tem seus próprio subelementos ou atributos (ou ambos), ou pai do subelemento tem mais de uma instância do subelemento como um filho. Caso contrário, a coluna é simple.

-   Quando há várias instâncias de um subelemento (pais diferentes), uma coluna é uma **registros** coluna se *qualquer* das instâncias implica um **Recordset** coluna; seu coluna é simple apenas se *todos os* instâncias implicam uma coluna simple.

-   Todos os **conjuntos de registros** têm uma coluna adicional chamada $Text.

 O código que é necessário para construir um **registros** é o seguinte:

```
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "http://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  O caminho do arquivo de dados pode ser especificado usando quatro convenções de nomenclatura diferentes.

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

 Assim que o **registros** tiver sido aberto, o ADO usual **registros** navegação comandos podem ser usados.

 **Conjuntos de registros** gerado pelo OSP tem algumas limitações:

-   Cursores do cliente (**adUseClient**) não têm suporte.

-   Hierárquica **conjuntos de registros** criado pela arbitrário XML não pode ser persistente usando **Recordset.Save**.

-   **Conjuntos de registros** criado com a OSP são somente leitura.

-   O XMLDSO adiciona uma coluna adicional de dados ($Text) a cada **registros** na hierarquia.

 Para obter mais informações sobre o provedor OLE DB simples, consulte [criar um provedor simples](http://msdn.microsoft.com/en-us/b31a6cba-58ae-4ee8-9039-700973d354d6).

## <a name="code-example"></a>Exemplo de código
 O seguinte código do Visual Basic demonstra a abrir um arquivo XML arbitrário, construindo hierárquico **registros**e recursivamente gravar cada registro de cada **registros** para a janela de depuração.

 Aqui está um arquivo XML simples que contém cotações de ações. O código a seguir usa esse arquivo para construir um nível de dois hierárquico **registros**.

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

 A seguir estão dois procedimentos do Visual Basic sub. O primeiro cria o **Recordset** e o transmite para o *WalkHier* quais recursivamente orienta na hierarquia, gravar cada procedimento sub **campo** em cada registro em cada **Registros** para a janela de depuração.

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
