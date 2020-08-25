---
description: 'Etapa 5: O DataControl é tornado utilizável (Tutorial RDS)'
title: 'Etapa 5: o DataControl é tornado utilizável (tutorial do RDS) | Microsoft Docs'
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 616b82b397694e4db41f709080dc4beafd945878
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759016"
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>Etapa 5: O DataControl é tornado utilizável (Tutorial RDS)
O objeto **Recordset** retornado está disponível para uso. Você pode examiná-lo, navegar ou editá-lo como faria com qualquer outro **conjunto de registros**. O que você pode fazer com o **conjunto de registros** depende do seu ambiente. Visual Basic e Visual C++ têm controles visuais que podem usar um **conjunto de registros** diretamente ou indiretamente com o auxílio de um controle de dados de habilitação.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por exemplo, se você estiver exibindo uma página da Web no Microsoft Internet Explorer, talvez queira exibir os dados do objeto **Recordset** em um controle visual. Os controles visuais em uma página da Web não podem acessar um objeto **Recordset** diretamente. No entanto, eles podem acessar o objeto **Recordset** por meio do [RDS. Controle](../../reference/rds-api/datacontrol-object-rds.md)de data. O **RDS. O DataControl** torna-se utilizável por um controle visual quando sua propriedade [SourceRecordset](../../reference/rds-api/recordset-sourcerecordset-properties-rds.md) é definida como o objeto **Recordset** .  
  
 O objeto de controle visual deve ter seu parâmetro **DATASRC** definido como **RDS. DataControl**e sua propriedade **DATAFLD** definida como um campo de objeto **Recordset** (coluna).  
  
 Neste tutorial, defina a propriedade **SourceRecordset** :  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Etapa 6: as alterações são enviadas ao servidor (tutorial do RDS)](./step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](./rds-tutorial-vbscript.md)