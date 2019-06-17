---
title: Cenário de persistência de conjunto de registros XML | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 893921a7100ca22cae219f5a0e88d543499053b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699700"
---
# <a name="xml-recordset-persistence-scenario"></a>Cenário de persistência do conjunto de registros XML
Nesse cenário, você criará um aplicativo de Active Server Pages (ASP) que salva o conteúdo de um objeto Recordset diretamente para o objeto de resposta do ASP.  
  
> [!NOTE]
>  Esse cenário requer que o servidor tem 5.0 de servidor de informações da Internet (IIS) ou posterior instalado.  
  
 O conjunto de registros retornado é exibido no Internet Explorer usando um [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md).  
  
 As etapas a seguir são necessárias para criar esse cenário:  
  
-   Configurar o aplicativo  
  
-   Obter os dados  
  
-   Enviar os dados  
  
-   Receber e exibir os dados  
  
## <a name="step-1-set-up-the-application"></a>Etapa 1: Configurar o aplicativo  
 Crie um diretório virtual do IIS denominado "XMLPersist" com permissões de script. Crie dois novos arquivos de texto na pasta para o qual o diretório virtual aponta, uma nomeada "XMLResponse.asp," a outros nomeado "default. htm."  
  
## <a name="step-2-get-the-data"></a>Etapa 2: Obter os dados  
 Nesta etapa, você irá escrever o código para abrir um conjunto de registros ADO e prepare para enviá-lo ao cliente. Abra o arquivo XMLResponse.asp com um editor de texto, como o bloco de notas e insira o código a seguir.  
  
```  
<%@ language="VBScript" %>  
  
<!-- #include file='adovbs.inc' -->  
  
<%  
  Dim strSQL, strCon  
  Dim adoRec   
  Dim adoCon   
  Dim xmlDoc   
  
  ' You will need to change "MySQLServer" below to the name of the SQL   
  ' server machine to which you want to connect.  
  strCon = "Provider=sqloledb;Data Source=MySQLServer;Initial Catalog=Pubs;Integrated Security=SSPI;"  
  Set adoCon = server.createObject("ADODB.Connection")  
  adoCon.Open strCon  
  
  strSQL = "SELECT Title, Price FROM Titles ORDER BY Price"  
  Set adoRec = Server.CreateObject("ADODB.Recordset")  
  adoRec.Open strSQL, adoCon, adOpenStatic, adLockOptimistic, adCmdText  
```  
  
 Certifique-se de alterar o valor da `Data Source` parâmetro no `strCon` para o nome do computador do Microsoft SQL Server.  
  
 Manter o arquivo aberto e vá para a próxima etapa.  
  
## <a name="step-3-send-the-data"></a>Etapa 3: Enviar os dados  
 Agora que você tem um conjunto de registros, você deve enviá-lo para o cliente, salvando-o como XML para o objeto de resposta do ASP. Adicione o seguinte código na parte inferior do XMLResponse.asp.  
  
```  
  Response.ContentType = "text/xml"  
  Response.Expires = 0  
  Response.Buffer = False  
  
  Response.Write "<?xml version='1.0'?>" & vbNewLine  
  adoRec.save Response, adPersistXML  
  adoRec.Close  
  Set adoRec=Nothing  
%>  
```  
  
 Observe que o objeto de resposta de ASP é especificado como o destino para o conjunto de registros [salvar método](../../../ado/reference/ado-api/save-method.md). O destino o método Save pode ser qualquer objeto que dá suporte à interface IStream, como o ADO [objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md), ou um nome de arquivo que inclui o caminho completo para o qual o conjunto de registros deve ser salva.  
  
 Salve e feche XMLResponse.asp antes de ir para a próxima etapa. Também copie o arquivo adovbs.inc da pasta de instalação da biblioteca de ADO padrão na mesma pasta onde você salvou o arquivo XMLResponse.asp.  
  
## <a name="step-4-receive-and-display-the-data"></a>Etapa 4: Receber e exibir os dados  
 Nesta etapa, você criará um arquivo HTML com um incorporado [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto que aponta para o arquivo XMLResponse.asp para obter o conjunto de registros. Abra default. htm com um editor de texto, como o bloco de notas e adicione o código a seguir. Substitua "sqlserver" na URL com o nome do seu servidor.  
  
```  
<HTML>  
<HEAD><TITLE>ADO Recordset Persistence Sample</TITLE></HEAD>  
<BODY>  
  
<TABLE DATASRC="#RDC1" border="1">  
  <TR>  
<TD><SPAN DATAFLD="title"></SPAN></TD>  
<TD><SPAN DATAFLD="price"></SPAN></TD>  
  </TR>  
</TABLE>  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="RDC1">  
   <PARAM NAME="URL" VALUE="XMLResponse.asp">  
</OBJECT>  
  
</BODY>  
</HTML>  
```  
  
 Feche o arquivo default. htm e salve-o na mesma pasta onde você salvou XMLResponse.asp. Usando o Internet Explorer 4.0 ou posterior, abra a URL https://*sqlserver*/XMLPersist/default.htm e observar os resultados. Os dados são exibidos em uma tabela vinculada do DHTML. Agora, abra a URL https:// *sqlserver* /XMLPersist/XMLResponse.asp e observar os resultados. O XML é exibido.  
  
## <a name="see-also"></a>Consulte também  
 [O método Save](../../../ado/reference/ado-api/save-method.md)   
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
