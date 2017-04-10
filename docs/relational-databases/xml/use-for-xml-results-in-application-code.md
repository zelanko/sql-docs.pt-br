---
title: "Usar resultados de FOR XML no c&#243;digo do aplicativo | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Cláusula FOR XML, o uso de código do aplicativo"
  - "XML [SQL Server], cláusula FOR XML"
  - "ASP.NET [SQL Server]"
  - ".NET Framework [SQL Server], dados de FOR XML"
  - "ADO [SQL Server]"
  - "ilhas de dados XML [SQL Server]"
  - "ilhas de dados [SQL Server]"
ms.assetid: 41ae67bd-ece9-49ea-8062-c8d658ab4154
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# Usar resultados de FOR XML no c&#243;digo do aplicativo
  Usando cláusulas FOR XML com consultas SQL, é possível recuperar e até converter resultados de consultas como dados XML. Essa funcionalidade permite fazer o seguinte quando os resultados da consulta FOR XML podem ser usados no código do aplicativo XML:  
  
-   Consultar tabelas SQL para instâncias de valores de [Dados XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
-   Aplicar a [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md) para retornar o resultado de consultas que contêm dados de tipo texto ou imagem como XML.  
  
 Este tópico fornece exemplos que demonstram essas aproximações.  
  
## Recuperando dados FOR XML com ilhas de dados ADO e XML  
 O objeto **Stream** do ADO ou outros objetos que dão suporte à interface **IStream** COM, como objetos **Request** e **Response** do ASP (Active Server Pages), pode ser usado para conter os resultados quando você está trabalhando com consultas FOR XML.  
  
 Por exemplo, o código ASP a seguir mostra os resultados de consulta a uma coluna de tipo de dados **xml** , Demographics, na tabela Sales.Store do banco de dados de exemplo AdventureWorks. Especificamente, a consulta procura o valor da instância dessa coluna da linha em que o CustomerID é igual a 3.  
  
```  
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<!-- %  Option Explicit      % -->  
<!-- 'Request.ServerVariables("SERVER_NAME") & ";" & _ -->  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Developer Studio"/>  
<META HTTP-EQUIV="Content-Type" content="text/html"; charset="iso-8859-1">  
<TITLE>FOR XML Query Example</TITLE>  
<STYLE>  
   BODY  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
   H3  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
</STYLE>  
  
<!-- #include file="adovbs.inc" -->  
<%  
   Response.Write "<H3>Server-side processing</H3>"  
   Response.Write "Page Generated @ " & Now() & "<BR/>"  
   Dim adoConn  
   Set adoConn = Server.CreateObject("ADODB.Connection")  
   Dim sConn  
   sConn = "Provider=SQLOLEDB;Data Source=(local);" & _  
            "Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
   Response.write "Connect String = " & sConn & "<BR/>"  
   adoConn.ConnectionString = sConn  
   adoConn.CursorLocation = adUseClient  
   adoConn.Open  
   Response.write "ADO Version = " & adoConn.Version & "<BR/>"  
   Response.write "adoConn.State = " & adoConn.State & "<BR/>"  
   Dim adoCmd  
   Set adoCmd = Server.CreateObject("ADODB.Command")  
   Set adoCmd.ActiveConnection = adoConn  
   Dim sQuery  
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO</sql:query></ROOT>"  
   Response.write "Query String = " & sQuery & "<BR/>"  
   Dim adoStreamQuery  
   Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
   adoStreamQuery.Open  
   adoStreamQuery.WriteText sQuery, adWriteChar  
   adoStreamQuery.Position = 0  
   adoCmd.CommandStream = adoStreamQuery  
   adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
   Response.write "Pushing XML to client for processing "  & "<BR/>"  
   adoCmd.Properties("Output Stream") = Response  
   Response.write "<XML ID='MyDataIsle'>"  
   adoCmd.Execute , , 1024  
   Response.write "</XML>"  
%>  
<SCRIPT language="VBScript" For="window" Event="onload">  
   Dim xmlDoc  
   Set xmlDoc = MyDataIsle.XMLDocument  
   Dim root  
   Set root = xmlDoc.documentElement.childNodes.Item(0).childNodes.Item(0).childNodes.Item(0)  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI><B>" & child.nodeName &  ":</B>  " & child.Text  & "</LI>"  
   Next  
   MsgBox xmlDoc.xml  
</SCRIPT>  
</HEAD>  
<BODY>  
   <H3>Client-side processing of XML Document MyDataIsle</H3>  
   <UL id=log>  
   </UL>  
</BODY>  
</HTML>  
<!-- EndRecordAndStreamVBS -->  
```  
  
 Essa página ASP de exemplo contém VBScript do lado do servidor que usa ADO para executar a consulta FOR XML e retorna os resultados XML em uma ilha de dados XML, MyDataIsle. Em seguida, essa ilha de dados XML é retornada no navegador para processamento adicional no lado do cliente. Código VBScript adicional no lado do cliente é usado para processar o conteúdo da ilha de dados XML. Esse processo é executado antes da exibição do conteúdo como parte do DHTML resultante e da abertura de uma caixa de mensagem para mostrar o conteúdo pré-processado da ilha de dados XML.  
  
#### Para testar este exemplo  
  
1.  Verifique se o IIS está instalado e se o banco de dados de exemplo do AdventureWorks para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi instalado.  
  
     Este exemplo requer que o Serviços de Informações da Internet (IIS) versão 5.0 ou posterior, esteja instalado com suporte do ASP habilitado. Além disso, o banco de dados de exemplo do AdventureWorks precisa estar instalado.  
  
2.  Copiar o exemplo de código fornecido anteriormente e colá-lo no XML ou no editor de texto usado. Salvar o arquivo como RetrieveResults.asp no diretório raiz usado para o IIS. Normalmente, o diretório é C:Inetpub\wwwroot.  
  
3.  Abra a página ASP em uma janela do navegador usando a seguinte URL. Primeiro, substitua 'MyServer' por "localhost" ou pelo nome real do servidor onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o IIS estão instalados.  
  
    ```  
    http://MyServer/RetrieveResults.asp  
    ```  
  
 Os resultados da página HTML gerada exibidos são semelhantes à seguinte saída de exemplo:  
  
##### Processamento no lado do servidor  
 Page Generated @ 3/11/2006 3:36:02 PM  
  
 Cadeia de Conexão = Provedor=SQLOLEDB;Fonte de Dados=MyServer;Catálogo Inicial=AdventureWorks;Segurança Integrada=SSPI;  
  
 Versão do ADO = 2.8  
  
 adoConn.State = 1  
  
 Cadeia de Caracteres da Consulta = SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO  
  
 Enviando XML por push ao cliente para processamento  
  
##### Processamento do lado do cliente do documento XML MyDataIsle  
  
-   **AnnualSales:** 1500000  
  
-   **AnnualRevenue:** 150000  
  
-   **BankName:** Primary International  
  
-   **BusinessType:** OS  
  
-   **YearOpened:** 1974  
  
-   **Specialty:** Road  
  
-   **SquareFeet:** 38000  
  
-   **Brands:** 3  
  
-   **Internet:** DSL  
  
-   **NumberEmployees:** 40  
  
 Em seguida, a caixa de mensagem do VBScript exibirá o seguinte conteúdo da ilha de dados XML original não filtrada que foi retornada pelos resultados da consulta XML.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Sales.Store>  
    <Demographics>  
      <StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
        <AnnualSales>1500000</AnnualSales>  
        <AnnualRevenue>150000</AnnualRevenue>  
        <BankName>Primary International</BankName>  
        <BusinessType>OS</BusinessType>  
        <YearOpened>1974</YearOpened>  
        <Specialty>Road</Specialty>  
        <SquareFeet>38000</SquareFeet>  
        <Brands>3</Brands>  
        <Internet>DSL</Internet>  
        <NumberEmployees>40</NumberEmployees>  
      </StoreSurvey>  
    </Demographics>  
  </Sales.Store>  
</ROOT>  
```  
  
## Recuperando dados FOR XML com o ASP.NET e o .NET Framework  
 Como no exemplo anterior, o seguinte código ASP.NET mostra os resultados da consulta de uma coluna de tipo de dados **xml** , Demographics, na tabela Sales.Store do banco de dados de exemplo AdventureWorks. Como no exemplo anterior, a consulta procura o valor da instância dessa coluna para a linha em que o CustomerID é igual a 3.  
  
 Neste exemplo, as seguintes APIs gerenciadas do Microsoft .NET Framework são usadas para executar o retorno e a renderização dos resultados de consultas FOR XML:  
  
1.  O**SqlConnection** é usado para abrir uma conexão ao SQL Server com base no conteúdo de uma variável da cadeia conexão especificada, strConn.  
  
2.  Em seguida, o**SqlDataAdapter** é usado como o adaptador de dados e usa a conexão SQL e a cadeia de caracteres de uma consulta SQL especificada para executar a consulta FOR XML.  
  
3.  Depois da execução da consulta, o método **SqlDataAdapter.Fill** é chamado e uma instância de um **DataSet,** MyDataSet, é passada para preencher o conjunto de dados com a saída da consulta FOR XML.  
  
4.  Em seguida, o método **DataSet.GetXml** é chamado para retornar os resultados da consulta como uma cadeia de caracteres que pode ser exibida na página HTML gerada pelo servidor.  
  
    ```  
    <%@ Page Language="VB" %>  
    <HTML>  
    <HEAD>  
    <TITLE>FOR XML Query Example</TITLE>  
    <STYLE>  
       BODY  
       {  
          FONT-FAMILY: Tahoma;  
          FONT-SIZE: 8pt;  
          OVERFLOW: auto  
       }  
       H3  
       {  
          FONT-FAMILY: Tahoma;  
          FONT-SIZE: 8pt;  
          OVERFLOW: auto  
       }  
    </STYLE>  
    </HEAD>  
    <BODY>  
    <%  
    Dim s as String  
    s = "<H3>Server-side processing</H3>" & _  
        "Page Generated @ " & Now() & "<BR/>"  
  
    Dim SQL As String   
    SQL = "SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO"  
  
    Dim strConn As String   
    strConn = "Server=(local);Database=AdventureWorks;Integrated Security=SSPI;"  
  
    Dim MySqlConn As New System.Data.SqlClient.SqlConnection(strConn)  
    Dim MySqlAdapter As New System.Data.SqlClient.SqlDataAdapter(SQL,MySqlConn)  
    Dim MyDataSet As New System.Data.DataSet  
  
    MySqlConn.Open()  
    s = s & "<P>SqlConnection opened.</P>"   
  
    MySqlAdapter.Fill(MyDataSet)  
    s = s & "<P>" & MyDataSet.GetXml  & "</P>"  
  
    MySqlConn.Close()  
    s = s & "<P>SqlConnection closed.</P>"   
  
    Message.InnerHtml=s  
    %>  
    <SPAN id="Message" runat=server />  
    </BODY>  
    </HTML>  
    ```  
  
#### Para testar este exemplo  
  
1.  Verifique se o IIS está instalado e se o banco de dados de exemplo do AdventureWorks para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi instalado.  
  
     Este exemplo requer que o Serviços de Informações da Internet (IIS) versão 5.0 ou posterior, esteja instalado com o suporte ao ASP.NET habilitado. Além disso, o banco de dados de exemplo do AdventureWorks precisa estar instalado.  
  
2.  Copiar o código fornecido anteriormente e colá-lo no XML ou no editor de texto usado. Salvar o arquivo como RetrieveResults.aspx no diretório raiz usado para o IIS. Normalmente, o diretório é C:Inetpub\wwwroot.  
  
3.  Abra a página ASP.NET em uma janela de navegador usando a seguinte URL. Primeiro, substitua 'MyServer' por "localhost" ou pelo nome real do servidor onde o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o IIS estão instalados.  
  
    ```  
    http://MyServer/RetrieveResults.aspx  
    ```  
  
 Os resultados da página HTML gerada exibidos são semelhantes à seguinte saída de exemplo:  
  
##### Processamento no lado do servidor  
  
```  
Page Generated @ 3/11/2006 3:36:02 PM  
  
SqlConnection opened.  
  
<Sales.Store><Demographics><StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey"><AnnualSales>1500000</AnnualSales><AnnualRevenue>150000</AnnualRevenue><BankName>Primary International</BankName><BusinessType>OS</BusinessType><YearOpened>1974</YearOpened><Specialty>Road</Specialty><SquareFeet>38000</SquareFeet><Brands>3</Brands><Internet>DSL</Internet><NumberEmployees>40</NumberEmployees></StoreSurvey></Demographics></Sales.Store>  
  
SqlConnection closed.  
```  
  
> [!NOTE]  
>  Em seguida, o método [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**xml** permite solicitar que o resultado de uma consulta FOR XML seja retornado como tipo de dados **xml** , em vez de string ou image, com a especificação da [diretiva TYPE](../../relational-databases/xml/type-directive-in-for-xml-queries.md). Quando a diretiva TYPE é usada em consultas FOR XML, ela fornece acesso programático aos resultados de FOR XML de maneira semelhante à mostrada em [Usar dados XML em aplicativos](../../relational-databases/xml/use-xml-data-in-applications.md).  
  
## Consulte também  
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  