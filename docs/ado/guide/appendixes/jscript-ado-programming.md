---
title: "Programação de ADO JScript | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- JScript
helpviewer_keywords:
- JScript programming in ADO
- ADO, JScript programming
ms.assetid: 62273658-0fe7-4aac-b4d8-f725e6baf043
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6ae8137c2e5641594c3ddcf768c47b7fe844fafc
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="jscript-ado-programming"></a>Programação de ADO do JScript
## <a name="creating-an-ado-project"></a>Criando um projeto de ADO  
 Microsoft JScript não oferece suporte a bibliotecas de tipo, portanto não é necessário para a referência ADO em seu projeto. Consequentemente, não há recursos associados como conclusão de linha de comando têm suporte. Além disso, por padrão, constantes enumerado do ADO não são definidos no JScript.  
  
 No entanto, o ADO fornece que incluir com dois arquivos que contém as definições a seguir para ser usado com JScript:  
  
-   Para uso em scripts do lado do servidor Adojavas.inc, que é instalado nas pastas de biblioteca do ADO.  
  
-   Para uso em scripts do lado do cliente Adcjavas.inc, que é instalado nas pastas de biblioteca do ADO.  
  
 Você pode copiar e colar definições de constantes desses arquivos em suas páginas ASP ou, se você estiver fazendo scripts de servidor, copie o arquivo de Adojavas.inc para uma pasta no seu site da Web e faz referência a ele na página ASP como este:  
  
```  
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>Criando objetos ADO em JScript  
 Você deve usar o **CreateObject** chamada de função:  
  
```  
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>Exemplo de JScript  
 O código a seguir é um exemplo genérico da programação do lado do servidor JScript em um arquivo de Active Server Page (ASP) que abre uma **registros** objeto:  
  
```  
<%  @LANGUAGE="JScript" %>  
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

