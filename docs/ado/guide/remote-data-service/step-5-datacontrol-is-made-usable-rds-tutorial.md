---
title: 'Etapa 5: DataControl é feita utilizável (Tutorial de RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], datacontrol made usable
ms.assetid: ed5c4a24-9804-4c85-817e-317652acb9b4
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 564c9b1984226c02ab1cb960ff6e4ed32b5527d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="step-5-datacontrol-is-made-usable-rds-tutorial"></a>Etapa 5: DataControl é feita utilizável (Tutorial de RDS)
Retornado **registros** objeto está disponível para uso. Você pode examinar, navegue ou editá-la como faria com qualquer outro **registros**. O que você pode fazer com o **registros** depende do ambiente. Visual Basic e Visual C++ tem controles visuais que podem usar um **registros** direta ou indiretamente com a Ajuda de um habilitar o controle de dados.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Por exemplo, se você estiver exibindo uma página da Web no Microsoft Internet Explorer, você talvez queira exibir o **registros** dados em um controle visual do objeto. Controles Visual em uma página da Web não podem acessar um **registros** diretamente do objeto. No entanto, eles podem acessar o **registros** objeto por meio de [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md). O **RDS. DataControl** se tornará utilizável por um visual controlar quando seu [SourceRecordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) está definida como o **registros** objeto.  
  
 O objeto de controle visual deve ter seu **DATASRC** parâmetro definido o **RDS. DataControl**e sua **DATAFLD** propriedade definida como um **registros** campo (coluna) do objeto.  
  
 Neste tutorial, defina o **SourceRecordset** propriedade:  
  
```  
Sub RDSTutorial5()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DC as New RDS.DataControl  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
   DC.SourceRecordset = RS         ' Visual controls can now bind to DC.  
...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Etapa 6: As alterações são enviadas ao servidor (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-6-changes-are-sent-to-the-server-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
