---
title: As configurações de cliente necessárias | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cec3e79e3d37f064cb742588519a374737e01319
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63191812"
---
# <a name="required-client-settings"></a>Configurações necessárias de cliente
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Especifique as seguintes configurações para usar um personalizado **DataFactory** manipulador.  
  
-   Especifique "provedor = Remote MS" na [o objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md) objeto [provedor de propriedade (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) propriedade ou o **Conexão** cadeia de caracteres de conexão do objeto "**Provedor**= "palavra-chave.  
  
-   Defina as [propriedade CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient**.  
  
-   Especifique o nome do manipulador a ser usado na [objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) do objeto **manipulador** propriedade, ou o [objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) cadeia de caracteres de conexão do objeto " **Manipulador**= "palavra-chave. (Você não pode definir o manipulador de **Conexão** cadeia de conexão do objeto.)  
  
 O RDS fornece um manipulador padrão no servidor chamado **MSDFMAP. Manipulador**. (O arquivo de personalização padrão é denominado MSDFMAP. INI).  
  
 **Exemplo**  
  
 Suponha que as seguintes seções **MSDFMAP. INI** e o nome da fonte de dados, AdvWorks, foram definidos anteriormente:  
  
```console
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 Os trechos de código a seguir são escritos em Visual Basic:  
  
## <a name="rdsdatacontrol-version"></a>RDS. Versão do DataControl  
  
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
  
 Especifique o [manipulador de propriedade (RDS)](../../../ado/reference/rds-api/handler-property-rds.md) propriedade ou a palavra-chave; o [provedor de propriedade (ADO)](../../../ado/reference/ado-api/provider-property-ado.md) propriedade ou a palavra-chave; e o *CustomerById* e  *CustomerDatabase* identificadores. Em seguida, abra o **Recordset** objeto  
  
 rs.Open "CustomerById(4)", "Handler=MSDFMAP.Handler;" & _  
  
```vb
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=https://yourServer"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Seção conexão do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Seção de UserList do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

