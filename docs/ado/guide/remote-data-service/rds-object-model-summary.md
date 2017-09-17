---
title: Resumo do modelo de objeto do RDS | Microsoft Docs
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
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1c89ea8ccd9875368ea0d279c54a1153bc0cfd3d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="rds-object-model-summary"></a>Resumo do modelo de objeto de RDS
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
|Objeto|Description|  
|------------|-----------------|  
|[RDS. Espaço de dados](../../../ado/reference/rds-api/dataspace-object-rds.md)|Este objeto contém um método para obter um proxy do servidor. O proxy pode ser o padrão ou um programa de servidor personalizado (objeto comercial). O programa do servidor pode ser chamado na Internet, intranet, uma rede local, ou uma biblioteca de vínculo dinâmico local.<br /><br /> O **DataSpace** objeto é seguro para script.|  
|[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|Esse objeto representa o programa de servidor padrão. Ele executa o comportamento de recuperação e atualização de dados do RDS padrão.<br /><br /> O **DataFactory** o objeto não é seguro para script.|  
|[RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|Esse objeto automaticamente pode invocar o **RDS. DataSpace** e **RDSServer.DataFactory** objetos.<br /><br /> Use esse objeto para invocar o comportamento de recuperação ou a atualização de dados do RDS padrão.<br /><br /> Esse objeto também fornece os meios para controles visuais acessar retornado **registros** objeto.<br /><br /> O **DataControl** objeto é seguro para script.|  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Cenário RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)



