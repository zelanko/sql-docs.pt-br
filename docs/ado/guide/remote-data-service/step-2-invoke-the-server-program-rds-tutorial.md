---
title: 'Etapa 2: Chamar o programa de servidor (Tutorial de RDS) | Microsoft Docs'
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
caps.latest.revision: "14"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2686f9206b49cd193cda9970aad72a10d75c482
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>Etapa 2: Chamar o programa de servidor (Tutorial de RDS)
Quando você invoca um método no cliente *proxy*, o método é executado o programa real no servidor. Nesta etapa, você poderá executar uma consulta no servidor.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 **A parte** se não houver [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) neste tutorial, a maneira mais conveniente de executar essa etapa seria usar o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto. O **RDS. DataControl** combina a etapa anterior de criar um proxy, com essa etapa, emite a consulta.  
  
 Definir o **RDS. DataControl** objeto [servidor](../../../ado/reference/rds-api/server-property-rds.md) propriedade para identificar onde o programa de servidor deve ser inicializado; o [conectar](../../../ado/reference/rds-api/connect-property-rds.md) propriedade para especificar a cadeia de conexão para acessar a fonte de dados; e o [SQL](../../../ado/reference/rds-api/sql-property.md) propriedade para especificar o texto do comando de consulta. Em seguida, emita o [atualizar](../../../ado/reference/rds-api/refresh-method-rds.md) método para fazer com que o programa do servidor para se conectar à fonte de dados, recuperar linhas especificadas pela consulta e retornar um **registros** objeto para o cliente.  
  
 Este tutorial não usa o **RDS. DataControl**, mas isso é como seria se tivesse:  
  
```  
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "http://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 Nem o tutorial invocar RDS com objetos ADO, mas isso é como seria se tivesse:  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=http://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **A parte B** o método geral de realizar esta etapa é chamar o **RDSServer.DataFactory** objeto [consulta](../../../ado/reference/rds-api/query-method-rds.md) método. Esse método usa uma cadeia de conexão, que é usada para conectar-se a uma fonte de dados, e um texto de comando, que é usado para especificar as linhas a serem retornados da fonte de dados.  
  
 Este tutorial usa o **DataFactory** objeto **consulta** método:  
  
```  
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Etapa 3: O servidor obtém um conjunto de registros (Tutorial de RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
