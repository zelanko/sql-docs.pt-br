---
title: Programação ADO JScript | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5e53f1d6e30497282cce8e895f458d81660240d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701297"
---
# <a name="jscript-ado-programming"></a>Programação ADO JScript
## <a name="creating-an-ado-project"></a>Criando um projeto do ADO  
 Microsoft JScript não oferece suporte a bibliotecas de tipos, para que você não precise referência ADO em seu projeto. Consequentemente, não há suporte para nenhum recurso associado, como a conclusão do linha de comando. Além disso, por padrão, constantes enumerado do ADO não são definidos no JScript.  
  
 No entanto, o ADO oferece que incluir com dois arquivos que contém as definições a seguir para ser usado com JScript:  
  
-   Para o uso de scripts de servidor Adojavas.inc, que é instalado nas pastas de biblioteca do ADO.  
  
-   Para o uso de scripts de cliente Adcjavas.inc, que é instalado nas pastas de biblioteca do ADO.  
  
 Você pode copiar e colar definições de constantes desses arquivos em suas páginas ASP ou, se você estiver fazendo a criação de scripts do lado do servidor, copie o arquivo de Adojavas.inc para uma pasta no seu site da Web e faz referência a ela da sua página ASP assim:  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>Criando objetos do ADO em JScript  
 Em vez disso, você deve usar o **CreateObject** chamada de função:  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>Exemplo de JScript  
 O código a seguir está um exemplo genérico da programação do lado do servidor de JScript em um arquivo de Active Server Page (ASP) que abre uma **Recordset** objeto:  
  
```javascript
<%  @LANGUAGE="JScript" %>  
<!--#include File="adojavas.inc"-->  
<HTML>  
<BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
<%  
var Source = "SELECT * FROM Authors";  
var Connect =  "Provider=sqloledb;Data Source=srv;" +  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
var Rs1 = Server.CreateObject( "ADODB.Recordset.2.5" );  
Rs1.Open(Source,Connect,adOpenForwardOnly);  
Response.Write("Success!");  
%>  
</BODY>  
</HTML>  
```
