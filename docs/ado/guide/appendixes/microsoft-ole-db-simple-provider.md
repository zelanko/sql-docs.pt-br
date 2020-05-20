---
title: Provedor simples do Microsoft OLE DB | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- simple provider [ADO]
- providers [ADO], OLE DB simple provider
- OLE DB simple provider [ADO]
ms.assetid: 1e7dc6f0-482c-4103-8187-f890865e40fc
author: rothja
ms.author: jroth
ms.openlocfilehash: 6e36648fe42024502316d65e3cf27412b907ffc2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761594"
---
# <a name="microsoft-ole-db-simple-provider-overview"></a>Visão geral do provedor simples do Microsoft OLE DB
O Microsoft OLE DB Simple Provider (OSP) permite que o ADO acesse todos os dados para os quais um provedor foi escrito usando o [Kit de ferramentas de OLE DB provedor (OSP) simples](https://msdn.microsoft.com/6e7b7931-9e4a-4151-ae51-672abd3f84a6). Provedores simples destinam-se a acessar fontes de dados que exigem apenas suporte fundamental OLE DB, como matrizes na memória ou documentos XML.

## <a name="connection-string-parameters"></a>Parâmetros de cadeia de conexão
 Para se conectar ao OLE DB DLL do provedor simples, defina o argumento do *provedor* como a propriedade [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) como:

```vb
MSDAOSP
```

 Esse valor também pode ser definido ou lido usando a propriedade [Provider](../../../ado/reference/ado-api/provider-property-ado.md) .

 Você pode se conectar a provedores simples que foram registrados como provedores de OLE DB completos usando o nome do provedor registrado, determinado pelo gravador do provedor.

## <a name="typical-connection-string"></a>Cadeia de conexão típica
 Uma cadeia de conexão típica para esse provedor é:

```vb
"Provider=MSDAOSP;Data Source=serverName"
```

 A cadeia de caracteres consiste nessas palavras-chave:

|Palavra-chave|Descrição|
|-------------|-----------------|
|**Provedor**|Especifica o provedor de OLE DB para SQL Server.|
|**Fonte de Dados**|Especifica o nome de um servidor.|

## <a name="xml-document-example"></a>Exemplo de documento XML
 O OLE DB provedor simples (OSP) no MDAC 2,7 ou posterior e no Windows Data Access Components (Windows DAC) foi aprimorado para dar suporte à abertura de **conjuntos de registros** ADO hierárquicos em arquivos XML arbitrários. Esses arquivos XML podem conter o esquema de persistência XML do ADO, mas não é necessário. Isso foi implementado conectando a OSP ao **MSXML2. dll**; Portanto, **MSXML2. dll** ou posterior é necessário.

 O arquivo **portfolio. xml** usado no exemplo a seguir contém a seguinte árvore:

```console
Portfolio
   Stock
      Shares
      Symbol
      Price
      Info
         Company Name
         WebSite
```

 O DSO XML usa heurística interna para converter os nós em uma árvore XML em capítulos em um **conjunto de registros**hierárquico.

 Usando essas heurísticas internas, a árvore XML é convertida em um **conjunto de registros** hierárquico de dois níveis do seguinte formato:

```console
Parent Recordset
Shares, Symbol, Price, $Text
   Child Recordset
      Company Name, WebSite, $Text
```

 Observe que as marcas de portfólio e informações não são representadas no **conjunto de registros**hierárquico. Para obter uma explicação de como o DSO XML converte as árvores XML em **conjuntos de registros**hierárquicos, consulte as regras a seguir. A coluna $Text é discutida na seção a seguir.

## <a name="rules-for-assigning-xml-elements-and-attributes-to-columns-and-rows"></a>Regras para atribuir elementos e atributos XML a colunas e linhas
 O DSO XML segue um procedimento para atribuir elementos e atributos a colunas e linhas em aplicativos associados a dados. O XML é modelado como uma árvore com uma marca que contém toda a hierarquia. Por exemplo, uma descrição XML de um livro pode conter marcas de capítulo, marcas de figura e marcas de seção. No nível mais alto, seria a marca Book, contendo o capítulo, a figura e a seção de subelementos. Quando o DSO XML mapeia elementos XML para linhas e colunas, os subelementos, não o elemento de nível superior, são convertidos.

 O DSO XML usa este procedimento para converter os subelementos:

-   Cada subelemento e atributo corresponde a uma coluna em algum **conjunto de registros** na hierarquia.

-   O nome da coluna é o mesmo que o nome do subelemento ou atributo, a menos que o elemento pai tenha um atributo e um subelemento com o mesmo nome; nesse caso, um "!" é anexado ao nome da coluna do subelemento.

-   Cada coluna é uma coluna *simples* que contém valores escalares (geralmente cadeias de caracteres) ou uma coluna de **conjunto de registros** que contém **conjuntos de registros**filhos.

-   As colunas correspondentes aos atributos são sempre simples.

-   As colunas correspondentes a subelementos são colunas do **conjunto de registros** se o subelemento tiver seus próprios subelementos ou atributos (ou ambos), ou se o pai do subelemento tiver mais de uma instância do subelemento como um filho. Caso contrário, a coluna será simples.

-   Quando houver várias instâncias de um subelemento (em pais diferentes), sua coluna será uma coluna de **conjunto de registros** se *qualquer* uma das instâncias implicasse uma coluna de conjunto de **registros** ; sua coluna será simples somente se *todas as* instâncias implicarem uma coluna simples.

-   Todos os **conjuntos de registros** têm uma coluna adicional denominada $Text.

 O código necessário para construir um conjunto de **registros** é o seguinte:

```vb
Dim adoConn as ADODB.Connection
Dim adoRS as ADODB.Recordset

Set adoRS = New ADODB.Connection
Set adoRS = New ADODB.Recordset

adoConn.Open "Provider=MSDAOSP; Data Source=MSXML2.DSOControl.2.6;"
adoRS.Open "https://WebServer/VRoot/portfolio.xml, adoConn
```

> [!NOTE]
>  O caminho do arquivo de dados pode ser especificado usando quatro convenções de nomenclatura diferentes.

```vb
'HTTP://
adoRS.Open "https://WebServer/VRoot/portfolio.xml", adoConn
'FILE://
adoRS.Open "file:/// C:\\Directory\\portfolio.xml", adoConn
'UNC Path
adoRS.Open "\\ComputerName\ShareName\portfolio.xml", adoConn
'Full DOS Path
adoRS.Open "C:\Directory\portfolio.xml", adoConn
```

 Assim que o **conjunto de registros** tiver sido aberto, os comandos usuais de navegação do **conjunto de registros** ADO podem ser usados.

 Os **conjuntos de registros** gerados pela OSP têm algumas limitações:

-   Não há suporte para cursores do cliente (**adUseClient**).

-   **Conjuntos de registros** hierárquicos criados em XML arbitrários não podem ser persistidos usando **Recordset. Save**.

-   Os **conjuntos de registros** criados com a OSP são somente leitura.

-   O XMLDSO adiciona uma coluna adicional de dados ($Text) a cada **conjunto de registros** na hierarquia.

 Para obter mais informações sobre o OLE DB provedor simples, consulte [criando um provedor simples](https://msdn.microsoft.com/b31a6cba-58ae-4ee8-9039-700973d354d6).

## <a name="code-example"></a>Exemplo de código
 O código Visual Basic a seguir demonstra como abrir um arquivo XML arbitrário, construir um **conjunto de registros**hierárquico e gravar recursivamente cada registro de cada **conjunto de registros** na janela de depuração.

 Aqui está um arquivo XML simples que contém Cotações de ações. O código a seguir usa esse arquivo para construir um **conjunto de registros**hierárquico de dois níveis.

```xml
<portfolio>
   <stock>
      <shares>100</shares>
      <symbol>MSFT</symbol>
      <price>$70.00</price>
      <info>
         <companyname>Microsoft Corporation</companyname>
         <website>https://www.microsoft.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>AAPL</symbol>
      <price>$107.00</price>
      <info>
         <companyname>Apple Computer, Inc.</companyname>
         <website>https://www.apple.com</website>
      </info>
   </stock>
   <stock>
      <shares>100</shares>
      <symbol>DELL</symbol>
      <price>$50.00</price>
      <info>
         <companyname>Dell Corporation</companyname>
         <website>https://www.dell.com</website>
      </info>
    </stock>
    <stock>
       <shares>100</shares>
       <symbol>INTC</symbol>
       <price>$115.00</price>
       <info>
          <companyname>Intel Corporation</companyname>
          <website>https://www.intel.com</website>
       </info>
   </stock>
</portfolio>
```

 A seguir estão dois procedimentos sub Visual Basic. O primeiro cria o **conjunto de registros** e o passa para o procedimento *WalkHier* sub, que percorre recursivamente a hierarquia, gravando cada **campo** em cada registro em cada **conjunto de registros** na janela de depuração.

```vb
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
    adoRS.Open "https://bwillett3/Kowalski/portfolio.xml", adoConn

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
