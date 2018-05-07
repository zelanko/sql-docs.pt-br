---
title: Tutorial RDS (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 02/14/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1681297e87731642b7f597e59c6d25ccb833c04d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="rds-tutorial-vbscript"></a>Tutorial RDS (VBScript)
Este é o Tutorial de RDS, gravado no Microsoft Visual Basic Scripting Edition. Para obter uma descrição do objetivo deste tutorial, consulte o [RDS Tutorial](../../../ado/guide/remote-data-service/rds-tutorial.md).  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Neste tutorial, [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) e [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) são criados em tempo de design — ou seja, elas são definidas com marcas de objetos, como este: `<OBJECT>...</OBJECT>`. Como alternativa, pode ser criados em tempo de execução com o [método CreateObject (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md) método. Por exemplo, o **RDS. DataControl** foi possível criar o objeto como este:  
  
```  
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
  
## <a name="step-1--specify-a-server-program"></a>Etapa 1 — Especifique um programa do servidor  
 VBScript pode descobrir o nome do servidor Web do IIS está em execução no acessando o VBScript **Request. ServerVariables** método disponível para o Active Server Pages:  
  
```  
"http://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 No entanto, para este tutorial, use o servidor imaginário, "Seu_servidor".  
  
> [!NOTE]
>  Preste atenção ao tipo de dados de **ByRef** argumentos. VBScript não permitem que você especifique o tipo de variável, portanto, você sempre deve transmitir um **Variant**. Ao usar HTTP, RDS permitirá que você passar uma variante para um método que esperava non-Variant se você chamá-lo com o **RDS. DataSpace** objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método. Ao usar DCOM ou um servidor em processo, você deve corresponder aos tipos de parâmetro dos lados do cliente e servidor, ou você receberá um erro de "Tipo incompatível".  
  
```  
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "http://yourServer")  
```  
  
## <a name="step-2a--invoke-the-server-program-with-rdsdatacontrol"></a>Etapa 2a: chamar o programa de servidor com RDS. DataControl  
 Este exemplo é simplesmente um comentário demonstra que o comportamento padrão da **RDS. DataControl** é executar a consulta especificada.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="http://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b--invoke-the-server-program-with-rdsserverdatafactory"></a>Etapa 2b: chamar o programa de servidor com RDSServer.DataFactory  
  
## <a name="step-3--server-obtains-a-recordset"></a>Etapa 3 — Servidor obtém um conjunto de registros  
  
## <a name="step-4--server-returns-the-recordset"></a>Etapa 4 — O servidor retorna o conjunto de registros  
  
```  
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5--datacontrol-is-made-usable-by-visual-controls"></a>Etapa 5 — DataControl é feita utilizável por controles visual  
  
```  
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a--changes-are-sent-to-the-server-with-rdsdatacontrol"></a>Etapa 6a — alterações são enviadas para o servidor de RDS. DataControl  
 Este exemplo é simplesmente um comentário demonstrando como o **RDS. DataControl** executa as atualizações.  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="http://yourServer/">  
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
  
## <a name="step-6b--changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>Etapa 6b, as alterações são enviadas para o servidor com RDSServer.DataFactory  
  
```  
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **Este é o fim do tutorial.**  
  
## <a name="see-also"></a>Consulte também  
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
