---
title: 'Etapa 2: Invocar o programa de servidor (Tutorial RDS) | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ca35b952cdb228e70a2e747026214dc1cf020f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922091"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>Etapa 2: Invocar o programa de servidor (Tutorial RDS)
Quando você invoca um método no cliente *proxy*, o programa real no servidor executa o método. Nesta etapa, você vai executar uma consulta no servidor.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 **A parte** se não houver [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) neste tutorial, a maneira mais conveniente para executar esta etapa seria usar o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto. O **RDS. DataControl** combina a etapa anterior de criação de um proxy, com essa etapa, emitindo a consulta.  
  
 Defina o **RDS. DataControl** objeto [Server](../../../ado/reference/rds-api/server-property-rds.md) propriedade para identificar em que o programa de servidor deve ser instanciado; o [Connect](../../../ado/reference/rds-api/connect-property-rds.md) propriedade para especificar a cadeia de conexão para acessar a fonte de dados; e o [SQL](../../../ado/reference/rds-api/sql-property.md) propriedade para especificar o texto do comando de consulta. Em seguida, execute o [Refresh](../../../ado/reference/rds-api/refresh-method-rds.md) método para fazer com que o programa de servidor para se conectar à fonte de dados, recuperar linhas especificadas pela consulta e retornar um **Recordset** objeto para o cliente.  
  
 Este tutorial não usa o **RDS. DataControl**, mas isso é como ela ficaria se tivesse:  
  
```vb
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "https://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 Nem o tutorial invocar RDS com objetos do ADO, mas isso é como ela ficaria se tivesse:  
  
```vb
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=https://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **A parte B** o método geral de realizar esta etapa é invocar o **RDSServer.DataFactory** objeto [consulta](../../../ado/reference/rds-api/query-method-rds.md) método. Esse método usa uma cadeia de conexão, que é usado para conectar-se a uma fonte de dados, e um texto de comando, que é usado para especificar as linhas a serem retornados da fonte de dados.  
  
 Este tutorial usa o **DataFactory** objeto **consulta** método:  
  
```vb
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Consulte também  
 [Etapa 3: Servidor obtém um conjunto de registros (Tutorial RDS)](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
