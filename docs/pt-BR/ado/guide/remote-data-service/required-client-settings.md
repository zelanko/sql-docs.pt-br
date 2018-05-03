---
title: As configurações de cliente necessárias | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a49cb0ead3d4f002761c05434521e6077cd2c54d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="required-client-settings"></a>Configurações de cliente necessárias
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Especifique as seguintes configurações para usar um personalizado **DataFactory** manipulador.  
  
-   Especifique "provedor = MS Remote" no [Conexão Object (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) objeto [provedor Property (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) propriedade ou o **Conexão** cadeia de caracteres de conexão do objeto "**Provedor**= "palavra-chave.  
  
-   Definir o [CursorLocation Property (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient**.  
  
-   Especifique o nome do manipulador a ser usado no [DataControl objeto (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto **manipulador** propriedade, ou o [Recordset Object (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) cadeia de conexão do objeto " **Manipulador**= "palavra-chave. (Você não pode definir o manipulador de **Conexão** cadeia de conexão do objeto.)  
  
 RDS fornece um manipulador padrão no servidor chamado **MSDFMAP. Manipulador de**. (O arquivo de personalização padrão é denominado MSDFMAP. INI).  
  
 **Exemplo**  
  
 Suponha que as seguintes seções **MSDFMAP. INI** e o nome da fonte de dados, AdvWorks, foi definido anteriormente:  
  
```  
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 Os trechos de código a seguir são escritos em Visual Basic:  
  
## <a name="rdsdatacontrol-version"></a>RDS. Versão DataControl  
  
```  
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "http://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>Versão do conjunto de registros  
  
```  
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 Especifique o [manipulador de propriedade (RDS)](../../../ado/reference/rds-api/handler-property-rds.md) propriedade ou palavra-chave; o [provedor Property (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) propriedade ou palavra-chave; e o *CustomerById* e  *CustomerDatabase* identificadores. Abra o **registros** objeto  
  
 RS. Abra "CustomerById(4)", "manipulador = MSDFMAP. Manipulador;"& _  
  
```  
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=http://yourServer"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Arquivo de personalização de conectar-se a seção](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção do arquivo UserList de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)






















