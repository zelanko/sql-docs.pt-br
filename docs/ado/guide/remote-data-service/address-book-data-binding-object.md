---
title: Objeto de associação de dados do catálogo de endereços | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 71b1897830c4a5382e6903f5e05aa29d1ce37d1b
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764727"
---
# <a name="address-book-data-binding-object"></a>Objeto de associação de dados do catálogo de endereço
O aplicativo de catálogo de endereços usa o [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) para associar dados do banco de dado SQL Server a um objeto visual (nesse caso, uma tabela DHTML) na página HTML do cliente do aplicativo. A lógica do programa VBScript orientada por eventos usa o [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) para:  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
-   Consulte o banco de dados, envie atualizações para o banco de dado e atualize a grade Data.  
  
-   Permitir que os usuários movam para o primeiro registro, próximo, anterior ou último na grade de dados.  
  
 O código a seguir define o **RDS. Componente DataControl** :  
  
```vb
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=DC1 Width=1 Height=1>  
   <PARAM NAME="SERVER" VALUE="https://<%=Request.ServerVariables("SERVER_NAME")%>">  
   <PARAM NAME="CONNECT" VALUE="Provider=sqloledb;  
Initial Catalog=AddrBookDb;Integrated Security=SSPI;">  
</OBJECT>  
```  
  
 A marca OBJECT define o **RDS. Componente DataControl** no programa. A marca inclui dois tipos de parâmetros:  
  
-   Os associados à marca de objeto genérico.  
  
-   Aqueles específicos para o **RDS. Objeto DataControl** .  
  
## <a name="generic-object-tag-parameters"></a>Parâmetros de marca de objeto genérico  
 A tabela a seguir descreve os parâmetros associados à marca OBJECT.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|***CLASSID***|Um número exclusivo de 128 bits que identifica o tipo de objeto inserido para o sistema. Esse identificador é mantido no registro do sistema do computador local. (Para as IDs de classe do **RDS. Objeto DataControl** , consulte [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md).)|  
|***ID***|Define um identificador de todo o documento para o objeto inserido que é usado para identificá-lo no código.|  
  
## <a name="rdsdatacontrol-tag-parameters"></a>Serviços. Parâmetros de marca do DataControl  
 A tabela a seguir descreve os parâmetros específicos para o **RDS. Objeto DataControl** . (Para obter uma lista completa de **RDS. **Parâmetros de objeto DataControl e quando implementá-los, consulte [RDS. Objeto DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md).)  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|[SERVIDOR](../../../ado/reference/rds-api/server-property-rds.md)|Se você estiver usando HTTP, o valor será o nome do computador do servidor precedido por `https://` .|  
|[CONNECT](../../../ado/reference/rds-api/connect-property-rds.md)|Fornece as informações de conexão necessárias para o **RDS. DataControl** para se conectar ao SQL Server.|  
|[SQL](../../../ado/reference/rds-api/sql-property.md)|Define ou retorna a cadeia de caracteres de consulta usada para recuperar o [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Botões de comando do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-command-buttons.md)


