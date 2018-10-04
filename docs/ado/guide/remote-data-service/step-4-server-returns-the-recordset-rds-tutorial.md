---
title: 'Etapa 4: O servidor retorna o conjunto de registros (Tutorial RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server returns Recordset
ms.assetid: 3d1855c4-419c-4810-b5ea-6c874b5e2905
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2edc9b1e0a235f10819f319cc68a595610a4e5d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783894"
---
# <a name="step-4-server-returns-the-recordset-rds-tutorial"></a>Etapa 4: O servidor retorna um conjunto de registros (Tutorial RDS)
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 RDS converte recuperada **conjunto de registros** objeto a um formulário que pode ser enviado de volta ao cliente (ou seja, ele *realiza marshaling* o **Recordset**). A forma exata da conversão e como ele será enviado depende se o servidor está na Internet ou em uma intranet, uma rede local, ou é uma biblioteca de vínculo dinâmico. No entanto, esse detalhe não é importante; tudo que importa é que RDS envia o **Recordset** volta ao cliente.  
  
 No lado do cliente, uma **Recordset** objeto é retornado e atribuído a uma variável local.  
  
```  
Sub RDSTutorial4()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Etapa 5: O DataControl é tornado utilizável (Tutorial RDS)](../../../ado/guide/remote-data-service/step-5-datacontrol-is-made-usable-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
