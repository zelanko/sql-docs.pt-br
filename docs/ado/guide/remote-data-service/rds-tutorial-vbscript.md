---
description: Tutorial RDS (VBScript)
title: Tutorial do RDS (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 6c8e93e72833e649f46ebda5885d3a16c5afece6
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759506"
---
# <a name="rds-tutorial-vbscript"></a>Tutorial RDS (VBScript)
Este é o tutorial do RDS, escrito no Microsoft Visual Basic Scripting Edition. Para obter uma descrição do objetivo deste tutorial, consulte o [tutorial do RDS](./rds-tutorial.md).  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Neste tutorial, o [RDS. DataControl](../../reference/rds-api/datacontrol-object-rds.md) e [RDS. O espaço de DataSpace](../../reference/rds-api/dataspace-object-rds.md) é criado em tempo de design – ou seja, eles são definidos com marcas de objeto, desta forma: `<OBJECT>...</OBJECT>` . Como alternativa, eles podem ser criados em tempo de execução com o método de [método CreateObject (RDS)](../../reference/rds-api/createobject-method-rds.md) . Por exemplo, o **RDS. O objeto DataControl** pode ser criado da seguinte maneira:  
  
```vb
Set DC = Server.CreateObject("RDS.DataControl")  
   <!-- RDS.DataControl -->  
   <OBJECT   
      ID="DC1" CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E33">  
   </OBJECT>  
  
   <!-- RDS.DataSpace -->  
   <OBJECT   
      ID="DS1" WIDTH=1 HEIGHT=1  
      CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
   </OBJECT>  
  
   <SCRIPT LANGUAGE="VBScript">  
  
   Sub RDSTutorial()  
   Dim DF1   
```  
  
## <a name="step-1---specify-a-server-program"></a>Etapa 1 – especificar um programa de servidor  
 O VBScript pode descobrir o nome do servidor Web do IIS no qual ele está sendo executado acessando o método de solicitação do VBScript **. ServerVariables** disponível para Active Server páginas:  
  
```vb
"https://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 No entanto, para este tutorial, use o servidor imaginário, "yourServer".  
  
> [!NOTE]
>  Preste atenção ao tipo de dados de argumentos **ByRef** . O VBScript não permite que você especifique o tipo de variável, portanto, você deve sempre passar uma **variante**. Ao usar HTTP, o RDS permitirá passar uma variante para um método que espera uma não variante se você a invocar com o **RDS. ** Método [CreateObject](../../reference/rds-api/createobject-method-rds.md) do objeto DataSpace. Ao usar o DCOM ou um servidor em processo, você deve corresponder aos tipos de parâmetro nos lados do cliente e do servidor ou receberá um erro de "incompatibilidade de tipo".  
  
```vb
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "https://yourServer")  
```  
  
## <a name="step-2a---invoke-the-server-program-with-rdsdatacontrol"></a>Etapa 2a – invocar o programa de servidor com RDS. DataControl  
 Este exemplo é meramente um comentário que demonstra que o comportamento padrão do **RDS. O DataControl** é para executar a consulta especificada.  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b---invoke-the-server-program-with-rdsserverdatafactory"></a>Etapa 2B – invocar o programa de servidor com RDSServer. datafactory  
  
## <a name="step-3---server-obtains-a-recordset"></a>Etapa 3-o servidor Obtém um conjunto de registros  
  
## <a name="step-4---server-returns-the-recordset"></a>Etapa 4-o servidor retorna o conjunto de registros  
  
```vb
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5---datacontrol-is-made-usable-by-visual-controls"></a>Etapa 5-o DataControl é tornado utilizável por controles visuais  
  
```vb
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a---changes-are-sent-to-the-server-with-rdsdatacontrol"></a>Etapa 6a – as alterações são enviadas para o servidor com RDS. DataControl  
 Este exemplo é meramente um comentário que demonstra como o **RDS. O DataControl** executa atualizações.  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial6A()  
Dim RS  
DC1.Refresh  
...  
Set RS = DC1.Recordset  
' Edit the Recordset object...  
' The SERVER and CONNECT properties are already set from Step 2A.  
Set DC1.SourceRecordset = RS  
...  
DC1.SubmitChanges  
```  
  
## <a name="step-6b---changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>Etapa 6B-as alterações são enviadas ao servidor com RDSServer. datafactory  
  
```vb
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **Este é o fim do tutorial.**  
  
## <a name="see-also"></a>Consulte Também  
 [Tutorial RDS](./rds-tutorial.md)