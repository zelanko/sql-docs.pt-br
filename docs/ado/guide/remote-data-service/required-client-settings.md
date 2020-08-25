---
description: Configurações necessárias de cliente
title: Configurações necessárias do cliente | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
author: rothja
ms.author: jroth
ms.openlocfilehash: 5263da344d39b828b431efd99a4171f74d2552db
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759376"
---
# <a name="required-client-settings"></a>Configurações necessárias de cliente
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Especifique as configurações a seguir para usar um manipulador de **DataFactory** personalizado.  
  
-   Especifique "provedor = MS remoto" na Propriedade do [objeto de conexão (](../../reference/ado-api/connection-object-ado.md) ADO [) ou](../../reference/ado-api/provider-property-ado.md) a palavra-chave da cadeia de conexão do objeto de **conexão** "**Provider**=".  
  
-   Defina a propriedade [CursorLocation (ADO)](../../reference/ado-api/cursorlocation-property-ado.md) como **adUseClient**.  
  
-   Especifique o nome do manipulador a ser usado na Propriedade do **manipulador** do objeto [DataControl (RDS)](../../reference/rds-api/datacontrol-object-rds.md) ou a palavra-chave "**Handler**=" da cadeia de conexão do objeto [Recordset (ADO)](../../reference/ado-api/recordset-object-ado.md) . (Não é possível definir o manipulador na cadeia de conexão do objeto **Connection** .)  
  
 O RDS fornece um manipulador padrão no servidor chamado **MSDFMAP. Manipulador**. (O arquivo de personalização padrão é denominado MSDFMAP.INI.)  
  
 **Exemplo**  
  
 Suponha que as seções a seguir em **MSDFMAP.INI** e o nome da fonte de dados, AdvWorks, foram definidas anteriormente:  
  
```console
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 Os trechos de código a seguir são gravados em Visual Basic:  
  
## <a name="rdsdatacontrol-version"></a>Serviços. Versão do DataControl  
  
```vb
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "https://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>Versão do conjunto de registros  
  
```vb
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 Especifique a propriedade ou palavra-chave da [Propriedade do manipulador (RDS)](../../reference/rds-api/handler-property-rds.md) ; a propriedade ou palavra-chave da [Propriedade do provedor (ADO)](../../reference/ado-api/provider-property-ado.md) ; e os identificadores *CustomerById* e *CustomerDatabase* . Em seguida, abra o objeto **Recordset**  
  
 RS. Abra "CustomerById (4)", "Handler = MSDFMAP. Handler; "& _  
  
```vb
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=https://yourServer"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Seção conexão de arquivo de personalização](./customization-file-connect-section.md)   
 [Seção SQL do arquivo de personalização](./customization-file-sql-section.md)   
 [Seção UserList do arquivo de personalização](./customization-file-userlist-section.md)   
 [Personalização de datafactory](./datafactory-customization.md)   
 [Configurações do cliente necessárias]()   
 [Noções básicas sobre o arquivo de personalização](./understanding-the-customization-file.md)   
 [Escrever seu próprio manipulador personalizado](./writing-your-own-customized-handler.md)