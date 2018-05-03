---
title: Programação de ADO VBScript | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ADO, VBScript
- VBScript [ADO]
ms.assetid: 6aaaf6d0-1376-4473-bea6-b81f2645a9ac
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 807029b5e5fc1861843806c6ccea9375467ec704
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="vbscript-ado-programming"></a>Programação de ADO VBScript
## <a name="creating-an-ado-project"></a>Criando um projeto de ADO  
 Microsoft Visual Basic, Scripting Edition não suporta bibliotecas de tipo, você não precisa fazer referência ADO em seu projeto. Consequentemente, não há recursos associados como conclusão de linha de comando têm suporte. Além disso, por padrão, constantes enumerado do ADO não são definidos no VBScript.  
  
 No entanto, o ADO fornece que incluir com dois arquivos que contém as definições para ser usado com o VBScript a seguir:  
  
-   Para uso em scripts do lado do servidor Adovbs.inc, que é instalado na pasta c:\Program Files\Common Files\System\ado\ por padrão.  
  
-   Para uso em scripts do lado do cliente Adcvbs.inc, que é instalado na pasta c:\Program Files\Common Files\System\msdac\ por padrão.  
  
 Você pode copiar e colar definições de constantes desses arquivos em suas páginas ASP ou, se você estiver fazendo scripts de servidor, copie o arquivo de Adovbs.inc para uma pasta no seu site da Web e fazer referência a ele na página ASP como este:  
  
```  
<!--#include File="adovbs.inc"-->  
```  
  
## <a name="creating-ado-objects-in-vbscript"></a>Criando objetos ADO no VBScript  
 Não é possível usar o **Dim** instrução atribuir objetos a um tipo específico no VBScript. Além disso, o VBScript não dá suporte a **novo** sintaxe usada com a **Dim** instrução no Visual Basic para aplicativos. Você deve usar o **CreateObject** chamada de função:  
  
```  
Dim Rs1  
Set Rs1 = Server.CreateObject( "ADODB.Recordset" )  
```  
  
## <a name="vbscript-examples"></a>Exemplos de VBScript  
 O código a seguir é um exemplo genérico da programação do VBScript do lado do servidor em um arquivo de página ASP (Active Server):  
  
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
  
## <a name="differences-between-vbscript-and-visual-basic"></a>Diferenças entre o VBScript e Visual Basic  
 Usando o ADO com o VBScript é semelhante a usar ADO com o Visual Basic de muitas maneiras, incluindo como sintaxe é usada. No entanto, existem algumas diferenças significativas:  
  
-   VBScript suporta apenas o tipo de dados de variante, que pode conter diferentes tipos de dados. Você pode armazenar os dados que necessários em um tipo de dados Variant e funcionem adequadamente os dados devido a conversão executada pelo VBScript. Ele reconhece o tipo exigido pelo ADO e converte o valor de variante adequadamente.  
  
-   Não é possível usar **no erro goto \<rótulo >** em VBScript.  
  
-   VBScript dá suporte a algumas das funções internas do Visual Basic, como **Msgbox**, **data**, e **IsNumeric**. Porém, como VBScript é um subconjunto do Visual Basic, nem todas as funções internas são suportadas. Por exemplo, o VBScript não dá suporte a **formato** função e as funções de e/s de arquivo.
