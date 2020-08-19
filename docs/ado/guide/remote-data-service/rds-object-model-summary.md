---
description: Resumo do modelo de objeto RDS
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d7488811326dda4228ef2f458b70d5575b33b122
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452138"
---
# <a name="rds-object-model-summary"></a>Resumo do modelo de objeto RDS
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
|Objeto|Descrição|  
|------------|-----------------|  
|[RDS.DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)|Este objeto contém um método para obter um proxy de servidor. O proxy pode ser o padrão ou um programa de servidor personalizado (objeto de negócios). O programa de servidor pode ser invocado na Internet, em uma intranet, em uma rede local ou em uma biblioteca de vínculo dinâmico local.<br /><br /> O objeto **DataSpace** é seguro para scripts.|  
|[RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)|Esse objeto representa o programa de servidor padrão. Ele executa a recuperação de dados padrão do RDS e o comportamento de atualização.<br /><br /> O objeto **DataFactory** não é seguro para scripts.|  
|[RDS.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)|Esse objeto pode invocar automaticamente o **RDS. Objetos DataSpace** e **RDSServer. datafactory** .<br /><br /> Use esse objeto para invocar o comportamento padrão de recuperação ou de atualização de dados RDS.<br /><br /> Esse objeto também fornece os meios para os controles visuais acessarem o objeto **Recordset** retornado.<br /><br /> O objeto **DataControl** é seguro para scripts.|  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Cenário de RDS](../../../ado/guide/remote-data-service/rds-scenario.md)   
 [Tutorial do RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [Segurança e uso RDS](../../../ado/guide/remote-data-service/rds-usage-and-security.md)


