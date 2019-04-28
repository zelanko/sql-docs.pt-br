---
title: SQL Server recursos preteridos no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4abd066dd2fc971528468fb7104cb0c11e088150
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843024"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>Recursos do SQL Server obsoletos no SQL Server 2014
  Este tópico descreve os recursos substituídos que ainda estão disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Esses recursos estão programados para serem removidos em uma versão futura do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Recursos preteridos não devem ser usados em aplicativos novos.  
  
## <a name="features-not-supported-in-the-next-version-of-includessnoversionincludesssnoversion-mdmd"></a>Recursos sem suporte na próxima versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Os recursos do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] a seguir não terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Não use esses recursos em novo trabalho de desenvolvimento e, assim que possível, modifique os aplicativos que os utilizam atualmente. A coluna Nome do recurso aparece em eventos de rastreamento como ObjectName, em contadores de desempenho e sys.dm_os_performance_counters como nome_da_instância. O ID do Recurso aparece em eventos de rastreamento como ObjectId.  
  
|Category|Recurso substituído|Substituição|Nome do recurso|ID do recurso|  
|--------------|------------------------|-----------------|------------------|----------------|  
|Programação de Dados|[sys.soap_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) ou ASP.NET|Serviços Web XML nativos|22|  
|Programação de Dados|[sys.endpoint_webmethods &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) ou ASP.NET|Serviços Web XML nativos|23|  
  
### <a name="slipstream-functionality"></a>Funcionalidade de instalação integrada  
 O recurso de Atualização de Produto substitui a funcionalidade de instalação integrada que estava disponível no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1. Portanto, os parâmetros de linha de comando /*PCUSource* e /*CUSource*, associados à funcionalidade de instalação integrada, não devem mais ser usados. Os parâmetros continuarão funcionando, mas poderão ser removidos em uma versão futura da Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . O parâmetro /*UpdateSource* combina a funcionalidade dos parâmetros Slipstream, /*PCUSource* e /*CUSource*.  
  
 Para obter mais informações sobre a funcionalidade de instalação integrada que estava disponível no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1, consulte [integrar uma atualização do SQL Server](https://go.microsoft.com/fwlink/?LinkId=219945) (https://go.microsoft.com/fwlink/?LinkId=219945).  
  
## <a name="see-also"></a>Consulte também  
 [Compatibilidade com versões anteriores](../../2014/getting-started/backward-compatibility.md)  
  
  
