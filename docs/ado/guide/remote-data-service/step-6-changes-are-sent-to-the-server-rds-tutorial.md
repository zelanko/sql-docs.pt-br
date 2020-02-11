---
title: 'Etapa 6: as alterações são enviadas ao servidor (tutorial RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a48b9c54496100bfe502bd496b12f35ced9ea8ee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922042"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>Etapa 6: As alterações são enviadas ao servidor (Tutorial RDS)
Se o objeto **Recordset** for editado, quaisquer alterações (ou seja, linhas adicionadas, alteradas ou excluídas) poderão ser enviadas de volta ao servidor.  
  
> [!NOTE]
>  O comportamento padrão de RDS pode ser invocado implicitamente com objetos ADO e o provedor de comunicação remota do Microsoft OLE DB. As consultas podem retornar o **conjunto de registros**s e os **conjuntos de registros**editados podem atualizar a fonte de dados. Este tutorial não invoca o RDS com objetos ADO, mas essa é a aparência que ele teria:  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **Parte A** Suponha que, nesse caso, você só tenha usado o [RDS. E que](../../../ado/reference/rds-api/datacontrol-object-rds.md) um objeto **Recordset** agora está associado ao **RDS. Controle**de data. O método [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) atualiza a fonte de dados com quaisquer alterações no objeto **Recordset** se as propriedades [Server](../../../ado/reference/rds-api/server-property-rds.md) e [Connect](../../../ado/reference/rds-api/connect-property-rds.md) ainda estiverem definidas.  
  
```vb
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "https://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **Parte B** Como alternativa, você pode atualizar o servidor com o objeto [RDSServer. datafactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) , especificando uma conexão e um objeto **Recordset** .  
  
```vb
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **Este é o fim do tutorial.**  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte Também  
 [Provedor de comunicação remota do Microsoft OLE DB (provedor de serviços ADO)](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [Tutorial do RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Tutorial RDS (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
