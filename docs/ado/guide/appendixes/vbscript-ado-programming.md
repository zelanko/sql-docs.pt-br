---
title: Programação ADO VBScript | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
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
manager: craigg
ms.openlocfilehash: 8fe2eb1d6d5c83a85fed628b02869cbf7b29eee4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47679994"
---
# <a name="vbscript-ado-programming"></a>Programação ADO VBScript
## <a name="creating-an-ado-project"></a>Criando um projeto do ADO  
 Microsoft Visual Basic, Scripting Edition não oferece suporte a bibliotecas de tipos, para que você não precise fazer referência ADO em seu projeto. Consequentemente, não há suporte para nenhum recurso associado, como a conclusão do linha de comando. Além disso, por padrão, constantes enumerado do ADO não são definidos no VBScript.  
  
 No entanto, o ADO oferece que incluir com dois arquivos que contém as definições a seguir para ser usado com VBScript:  
  
-   Para o uso de scripts de servidor Adovbs.inc, que é instalado na pasta c:\Program Files\Common Files\System\ado\ por padrão.  
  
-   Para o uso de scripts de cliente Adcvbs.inc, que é instalado na pasta c:\Program Files\Common Files\System\msdac\ por padrão.  
  
 Você pode copiar e colar definições de constantes desses arquivos em suas páginas ASP ou, se você estiver fazendo a criação de scripts do lado do servidor, copie o arquivo de Adovbs.inc para uma pasta no seu site da Web e referencie-a da sua página ASP assim:  
  
```  
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>Criar objetos do ADO no VBScript  
 Não é possível usar o **Dim** instrução atribuir objetos a um tipo específico no VBScript. Além disso, o VBScript não oferece suporte a **New** sintaxe usada com o **Dim** instrução no Visual Basic for Applications. Em vez disso, você deve usar o **CreateObject** chamada de função:  
  
```  
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>Exemplos de VBScript  
 O código a seguir está um exemplo genérico da programação do lado do servidor de VBScript em um arquivo de Active Server Page (ASP):  
  
```  
<%  @LANGUAGE="VBSCRIPT" %>  
<%  Option Explicit %>  
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
  
 Exemplos de VBScript mais específicos são incluídos na documentação do ADO. Para obter mais informações, consulte [exemplos de código ADO no Microsoft Visual Basic Scripting Edition](../../../ado/reference/ado-api/ado-code-examples-vbscript.md).  
  
## <a name="differences-between-vbscript-and-visual-basic"></a>Diferenças entre o VBScript e o Visual Basic  
 Usando o ADO com o VBScript é semelhante a usar o ADO com o Visual Basic de várias maneiras, incluindo como a sintaxe é usada. No entanto, existem algumas diferenças significativas:  
  
-   VBScript dá suporte a apenas o tipo de dados de variante, que pode conter diferentes tipos de dados. Você pode armazenar os dados que necessários em um tipo de dados Variant e os dados funcionarão corretamente devido à conversão de realizada pelo VBScript. Ele reconhece o tipo exigido pelo ADO e converte o valor na variante adequadamente.  
  
-   Não é possível usar **no erro goto \<rótulo >** dentro do VBScript.  
  
-   VBScript dá suporte a algumas das funções internas do Visual Basic, como **Msgbox**, **data**, e **IsNumeric**. No entanto, como o VBScript é um subconjunto do Visual Basic, nem todas as funções internas têm suporte. Por exemplo, o VBScript não dá suporte a **formato** função e as funções de e/s de arquivo.
