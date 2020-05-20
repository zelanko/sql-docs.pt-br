---
title: 'Etapa 2: invocar o programa de servidor (tutorial RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: rothja
ms.author: jroth
ms.openlocfilehash: c0e85b276ed8cc38419035d48357180c7952ff98
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764677"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>Etapa 2: Invocar o programa de servidor (Tutorial RDS)
Quando você invoca um método no *proxy*do cliente, o programa real no servidor executa o método. Nesta etapa, você executará uma consulta no servidor.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 **Parte A** Se você não estivesse usando [RDSServer. datafactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) neste tutorial, a maneira mais conveniente de executar essa etapa seria usar o [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) . O **RDS. O DataControl** combina a etapa anterior de criação de um proxy, com esta etapa, emitindo a consulta.  
  
 Defina o **RDS. **Propriedade do [servidor](../../../ado/reference/rds-api/server-property-rds.md) de objeto DataControl para identificar onde o programa do servidor deve ser instanciado; a propriedade [Connect](../../../ado/reference/rds-api/connect-property-rds.md) para especificar a cadeia de conexão para acessar a fonte de dados; e a propriedade [SQL](../../../ado/reference/rds-api/sql-property.md) para especificar o texto do comando de consulta. Em seguida, emita o método [Refresh](../../../ado/reference/rds-api/refresh-method-rds.md) para fazer com que o programa do servidor se conecte à fonte de dados, recupere as linhas especificadas pela consulta e retorne um objeto **Recordset** para o cliente.  
  
 Este tutorial não usa o **RDS. O DataControl**, mas é assim que se pareceria com:  
  
```vb
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "https://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 Nem o tutorial invoca o RDS com os objetos ADO, mas é assim que ele seria semelhante a:  
  
```vb
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=https://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **Parte B** O método geral de executar essa etapa é invocar o método de [consulta](../../../ado/reference/rds-api/query-method-rds.md) do objeto **RDSServer. datafactory** . Esse método usa uma cadeia de conexão, que é usada para se conectar a uma fonte de dados e um texto de comando, que é usado para especificar as linhas a serem retornadas da fonte de dados.  
  
 Este tutorial usa o método de **consulta** do objeto **DataFactory** :  
  
```vb
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Etapa 3: o servidor Obtém um conjunto de registros (tutorial RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
