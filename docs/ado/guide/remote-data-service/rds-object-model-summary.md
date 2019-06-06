---
title: Resumo do modelo de objeto RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS objects [ADO], object model summary
- RDS object model [ADO]
ms.assetid: 909f9af7-31db-4eec-ad52-650ce74dac2f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 434c27f5e2da0208ba5141664ccc69accfc2fbb2
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704241"
---
# <a name="rds-object-model-summary"></a>Resumo do modelo de objeto RDS
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
|Object|Descrição|  
|------------|-----------------|  
|[RDS.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)|Este objeto contém um método para obter um proxy do servidor. O proxy pode ser o padrão ou um programa de servidor personalizado (objeto de negócios). O programa de servidor pode ser invocado em Internet, intranet, uma rede local, ou ser uma biblioteca de vínculo dinâmico local.<br /><br /> O **DataSpace** objeto é seguro para script.|  
|[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|Este objeto representa o programa de servidor padrão. Ele executa o comportamento de recuperação e de atualização de dados do RDS padrão.<br /><br /> O **DataFactory** objeto não é seguro para script.|  
|[RDS.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|Esse objeto pode invocar automaticamente os **RDS. DataSpace** e **RDSServer.DataFactory** objetos.<br /><br /> Use esse objeto para invocar o comportamento de atualização ou de recuperação de dados do RDS padrão.<br /><br /> Esse objeto também fornece os meios para controles do visual acessar retornado **Recordset** objeto.<br /><br /> O **DataControl** objeto é seguro para script.|  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Cenário RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


