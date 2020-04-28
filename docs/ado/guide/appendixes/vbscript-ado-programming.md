---
title: Programação ADO do VBScript | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f242a3596735a4bc43256d05b87100e71295a3da
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926434"
---
# <a name="vbscript-ado-programming"></a>Programação ADO VBScript
## <a name="creating-an-ado-project"></a>Criando um projeto ADO  
 O Microsoft Visual Basic, Scripting Edition, não oferece suporte a bibliotecas de tipos, portanto, você não precisa fazer referência ao ADO em seu projeto. Consequentemente, não há suporte para nenhum recurso associado, como a conclusão da linha de comando. Além disso, por padrão, as constantes enumeradas do ADO não são definidas no VBScript.  
  
 No entanto, o ADO fornece dois arquivos de inclusão contendo as seguintes definições a serem usadas com o VBScript:  
  
-   Para scripts do lado do servidor, use Adovbs. Inc, que é instalado na pasta c:\Program Files\Common Files\System\ado\ por padrão.  
  
-   Para scripts do lado do cliente, use Adcvbs. Inc, que é instalado na pasta c:\Program Files\Common Files\System\msdac\ por padrão.  
  
 Você pode copiar e colar definições constantes desses arquivos em suas páginas ASP ou, se você estiver fazendo scripts do lado do servidor, copie o arquivo Adovbs. Inc para uma pasta no seu site e faça referência a ele em sua página ASP como esta:  
  
```vb
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>Criando objetos ADO em VBScript  
 Você não pode usar a instrução **Dim** para atribuir objetos a um tipo específico em VBScript. Além disso, o VBScript não oferece suporte à **nova** sintaxe usada com a instrução **Dim** em Visual Basic for Applications. Em vez disso, você deve usar a chamada de função **CreateObject** :  
  
```vb
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>Exemplos de VBScript  
 O código a seguir é um exemplo genérico de programação do lado do servidor VBScript em um arquivo de Active Server página (ASP):  
  
```vb
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
<!--#include File="adovbs.inc"-->  
<HTML>  
    <BODY BGCOLOR="White" topmargin="10" leftmargin="10">  
  
    <!-- Your ASP Code goes here -->  
<%  
Dim Source  
Dim Connect  
Dim Rs1  
  
Source = "SELECT * FROM Authors"  
Connect = "Provider=sqloledb;Data Source=srv;" & _  
    "Initial Catalog=Pubs;Integrated Security=SSPI;"  
  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
Rs1.Open Source, Connect, adOpenForwardOnly  
Response.Write("Success!")  
%>  
    </BODY>  
</HTML>  
```  
  
 Exemplos de VBScript mais específicos estão incluídos na documentação do ADO. Para obter mais informações, consulte [exemplos de código ADO no Microsoft Visual Basic Scripting Edition](../../../ado/reference/ado-api/ado-code-examples-vbscript.md).  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>Diferenças entre o VBScript e o Visual Basic  
 O uso do ADO com VBScript é semelhante ao uso do ADO com Visual Basic de várias maneiras, incluindo como a sintaxe é usada. No entanto, existem algumas diferenças significativas:  
  
-   O VBScript dá suporte apenas ao tipo de dados Variant, que pode conter diferentes tipos de dados. Você pode armazenar os dados necessários em um tipo de dados Variant e os dados funcionarão adequadamente devido à conversão realizada pelo VBScript. Ele reconhece o tipo exigido pelo ADO e converte o valor em Variant de acordo.  
  
-   Não é possível usar o **rótulo \<on Error GoTo>** no VBScript.  
  
-   O VBScript dá suporte a algumas das funções Visual Basic internas, como **MsgBox**, **Date**e **ISNUMERIC**. No entanto, como o VBScript é um subconjunto de Visual Basic, nem todas as funções internas têm suporte. Por exemplo, o VBScript não oferece suporte à função **Format** e às funções de e/s de arquivo.
