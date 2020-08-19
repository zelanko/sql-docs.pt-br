---
description: Programação ADO JScript
title: Programação ADO do JScript | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2f1cad0a2717bb652759a7c8b0d60efc4b3f4541
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444558"
---
# <a name="jscript-ado-programming"></a>Programação ADO JScript
## <a name="creating-an-ado-project"></a>Criando um projeto ADO  
 O Microsoft JScript não oferece suporte a bibliotecas de tipos, portanto, você não precisa fazer referência ao ADO em seu projeto. Consequentemente, não há suporte para nenhum recurso associado, como a conclusão da linha de comando. Além disso, por padrão, as constantes enumeradas do ADO não são definidas no JScript.  
  
 No entanto, o ADO fornece dois arquivos de inclusão que contêm as seguintes definições a serem usadas com o JScript:  
  
-   Para scripts do lado do servidor, use Adojavas. Inc, que é instalado nas pastas da biblioteca do ADO.  
  
-   Para scripts do lado do cliente, use Adcjavas. Inc, que é instalado nas pastas da biblioteca do ADO.  
  
 Você pode copiar e colar definições constantes desses arquivos em suas páginas ASP ou, se você estiver fazendo scripts do lado do servidor, copie o arquivo Adojavas. Inc para uma pasta no seu site e faça referência a ele em sua página ASP como esta:  
  
```javascript
<!--#include File="adojavas.inc"-->  
```  
  
## <a name="creating-ado-objects-in-jscript"></a>Criando objetos ADO no JScript  
 Em vez disso, você deve usar a chamada de função **CreateObject** :  
  
```javascript
var Rs1;  
Rs1 = Server.CreateObject("ADODB.Recordset");  
```  
  
## <a name="jscript-example"></a>Exemplo de JScript  
 O código a seguir é um exemplo genérico de programação do lado do servidor do JScript em um arquivo de Active Server página (ASP) que abre um objeto **Recordset** :  
  
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
