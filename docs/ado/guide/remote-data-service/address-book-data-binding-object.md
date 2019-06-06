---
title: O objeto de associação de dados do catálogo de endereços | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 31efe56dcb5ae926d5da08aa00a1005597b17b91
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66718623"
---
# <a name="address-book-data-binding-object"></a>Objeto de associação de dados do catálogo de endereço
O aplicativo de catálogo de endereços usa o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto ao qual associar dados do banco de dados do SQL Server a um objeto visual (no caso, uma tabela DHTML) na página de cliente HTML do aplicativo. A lógica do programa de VBScript controlada por evento usa o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) para:  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
-   Consultar o banco de dados, enviar atualizações para o banco de dados e atualizar a grade de dados.  
  
-   Permitir que os usuários mover para o primeiro, em seguida, anterior, ou o último registro na grade de dados.  
  
 O código a seguir define o **RDS. DataControl** componente:  
  
```vb
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 A marca de objeto define o **RDS. DataControl** componente no programa. A marca inclui dois tipos de parâmetros:  
  
-   Os associados com a marca de objeto genérica.  
  
-   Aqueles específicos para o **RDS. DataControl** objeto.  
  
## <a name="generic-object-tag-parameters"></a>Parâmetros de Tag do objeto genérico  
 A tabela a seguir descreve os parâmetros associados à marca de objeto.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|***CLASSID***|Um número exclusivo, de 128 bits que identifica o tipo do objeto inserido no sistema. Esse identificador é mantido no registro do sistema do computador local. (Para as IDs de classe do **RDS. DataControl** do objeto, consulte [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md).)|  
|***ID***|Define um identificador de todo o documento para o objeto incorporado que é usado para identificá-lo no código.|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDS. Parâmetros de Tag DataControl  
 A tabela a seguir descreve os parâmetros específicos para o **RDS. DataControl** objeto. (Para obter uma lista completa da **RDS. DataControl** parâmetros e quando implementá-los, consulte objeto [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md).)  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|[SERVER](../../../ado/reference/rds-api/server-property-rds.md)|Se você estiver usando HTTP, o valor é o nome do computador servidor precedido por `https://`.|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|Fornece as informações de conexão necessárias para o **RDS. DataControl** para se conectar ao SQL Server.|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|Define ou retorna a cadeia de caracteres de consulta usada para recuperar o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Botões de comando do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


