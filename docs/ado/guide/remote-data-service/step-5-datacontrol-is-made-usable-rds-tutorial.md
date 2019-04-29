---
title: 'Etapa 5: DataControl é tornado utilizável (Tutorial RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01b7a1b7829ace46cac7be21d33d9837845db9a7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62955766"
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>Etapa 5: O DataControl é tornado utilizável (Tutorial RDS)
Retornado **Recordset** objeto está disponível para uso. Você pode examinar, navegue ou editá-lo como faria com qualquer outro **conjunto de registros**. O que você pode fazer com o **Recordset** depende do ambiente. Visual Basic e Visual C++ têm controles visuais que podem usar um **Recordset** direta ou indiretamente com o auxílio de um controle de dados de habilitação.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por exemplo, se você estiver exibindo uma página da Web no Microsoft Internet Explorer, você talvez queira exibir o **Recordset** dados em um controle visual do objeto. Controles visuais em uma página da Web não é possível acessar uma **Recordset** diretamente do objeto. No entanto, eles podem acessar o **conjunto de registros** por meio do objeto a [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md). O **RDS. DataControl** se torna utilizável por um elemento visual controlar quando seus [SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) estiver definida como o **conjunto de registros** objeto.  
  
 O objeto visual do controle deve ter sua **DATASRC** parâmetro definido como o **RDS. DataControl**e sua **DATAFLD** propriedade definida como um **conjunto de registros** campo (coluna) do objeto.  
  
 Neste tutorial, defina as **SourceRecordset** propriedade:  
  
```vb
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Etapa 6: As alterações são enviadas ao servidor (Tutorial RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
