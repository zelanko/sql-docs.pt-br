---
title: Cenário de persistência do conjunto de registros XML | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4a1110db8505a2a721c3503e51276cfb895fb965
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748309"
---
# <a name="xml-recordset-persistence-scenario"></a>Cenário de persistência do conjunto de registros XML
Nesse cenário, você criará um aplicativo de páginas de Active Server (ASP) que salva o conteúdo de um objeto Recordset diretamente no objeto de resposta ASP.  
  
> [!NOTE]
>  Este cenário requer que o servidor tenha o Internet Information Server 5,0 (IIS) ou posterior instalado.  
  
 O conjunto de registros retornado é exibido no Internet Explorer usando um [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md).  
  
 As etapas a seguir são necessárias para criar este cenário:  
  
-   Configurar o aplicativo  
  
-   Obter os dados  
  
-   Enviar os dados  
  
-   Receber e exibir os dados  
  
## <a name="step-1-set-up-the-application"></a>Etapa 1: configurar o aplicativo  
 Crie um diretório virtual do IIS chamado "xmlpersist" com permissões de script. Crie dois novos arquivos de texto na pasta para a qual os pontos do diretório virtual, um chamado "xmlresponse. asp", o outro chamado "default. htm".  
  
## <a name="step-2-get-the-data"></a>Etapa 2: obter os dados  
 Nesta etapa, você escreverá o código para abrir um conjunto de registros ADO e se preparar para enviá-lo ao cliente. Abra o arquivo xmlresponse. asp com um editor de texto, como o bloco de notas, e insira o código a seguir.  
  
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
  
 Certifique-se de alterar o valor do `Data Source` parâmetro `strCon` para o nome do seu computador Microsoft SQL Server.  
  
 Mantenha o arquivo aberto e vá para a próxima etapa.  
  
## <a name="step-3-send-the-data"></a>Etapa 3: enviar os dados  
 Agora que você tem um conjunto de registros, deve enviá-lo para o cliente salvando-o como XML no objeto de resposta ASP. Adicione o seguinte código à parte inferior de xmlresponse. ASP.  
  
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
  
 Observe que o objeto de resposta ASP é especificado como o destino para o [método Save](../../../ado/reference/ado-api/save-method.md)do conjunto de registros. O destino do método Save pode ser qualquer objeto que dê suporte à interface IStream, como um [ADO (objeto de fluxo ADO)](../../../ado/reference/ado-api/stream-object-ado.md)ou um nome de arquivo que inclua o caminho completo para o qual o conjunto de registros deve ser salvo.  
  
 Salve e feche xmlresponse. asp antes de ir para a próxima etapa. Copie também o arquivo adovbs. Inc da pasta de instalação padrão da biblioteca do ADO para a mesma pasta em que você salvou o arquivo xmlresponse. ASP.  
  
## <a name="step-4-receive-and-display-the-data"></a>Etapa 4: receber e exibir os dados  
 Nesta etapa, você criará um arquivo HTML com um objeto de [controle de objeto de DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) inserido que aponta para o arquivo xmlresponse. asp para obter o conjunto de registros. Abra o default. htm com um editor de texto, como o bloco de notas, e adicione o código a seguir. Substitua "SqlServer" na URL pelo nome do seu servidor.  
  
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
  
 Feche o arquivo default. htm e salve-o na mesma pasta em que você salvou xmlresponse. ASP. Usando o Internet Explorer 4,0 ou posterior, abra a URL https://*SqlServer*/XMLPersist/default.htm e observe os resultados. Os dados são exibidos em uma tabela de DHTML associada. Agora, abra a URL https:// *SqlServer* /XMLPersist/XMLResponse.asp e observe os resultados. O XML é exibido.  
  
## <a name="see-also"></a>Consulte Também  
 [Salvar método](../../../ado/reference/ado-api/save-method.md)   
 [Persistência de registros em formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
