---
title: "Objeto de associação de dados do catálogo de endereços | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS scenarios [ADO], data-binding object
- address book application scenario [ADO], data-binding object
ms.assetid: 080c1925-d453-4b89-92ac-c93591490518
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 644180448474d2c07b1f53b570e25ac39074edfb
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="address-book-data-binding-object"></a>Objeto de associação de dados de catálogo de endereço
O aplicativo de catálogo de endereços usa o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto para associar dados do banco de dados do SQL Server a um objeto visual (no caso, uma tabela DHTML) na página de cliente HTML do aplicativo. A lógica de programação controlada por evento VBScript usa o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) para:  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
-   Consultar o banco de dados, enviar atualizações para o banco de dados e atualizar a grade de dados.  
  
-   Permitir que os usuários para mover para o primeiro, em seguida, anterior, ou o último registro na grade de dados.  
  
 O código a seguir define o **RDS. DataControl** componente:  
  
```  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="http://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 Define a marca do objeto de **RDS. DataControl** componente no programa. A marca inclui dois tipos de parâmetros:  
  
-   Os associados com a marca do objeto genérica.  
  
-   Perguntas específicas a **RDS. DataControl** objeto.  
  
## <a name="generic-object-tag-parameters"></a>Parâmetros de marca de objeto genérico  
 A tabela a seguir descreve os parâmetros associados a marca do objeto.  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|***IDENTIFICAÇÃO DE CLASSE***|Um número exclusivo de 128 bits que identifica o tipo de objeto inserido no sistema. Esse identificador é mantido no registro do sistema do computador local. (Para as IDs de classe do **RDS. DataControl** de objeto, consulte [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md).)|  
|***ID***|Define um identificador de todo o documento para o objeto incorporado que é usado para identificá-lo no código.|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>RDS. Parâmetros de marca DataControl  
 A tabela a seguir descreve os parâmetros específicos para o **RDS. DataControl** objeto. (Para obter uma lista completa do **RDS. DataControl** objeto parâmetros e quando implementá-las, consulte [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md).)  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|[SERVIDOR](../../../ado/reference/rds-api/server-property-rds.md)|Se você estiver usando HTTP, o valor é o nome do computador do servidor precedido por `http://`.|  
|[CONECTE-SE](../../../ado/reference/rds-api/connect-property-rds.md)|Fornece as informações de conexão necessárias para o **RDS. DataControl** para se conectar ao SQL Server.|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|Define ou retorna a cadeia de caracteres de consulta usada para recuperar o [registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Botões de comando do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-command-buttons.md)



