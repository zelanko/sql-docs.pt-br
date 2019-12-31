---
title: Recursos de SQL Server preteridos no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44fbab98aa017be66cd4dc369a713f44e8d248d5
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228223"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>Recursos do SQL Server obsoletos no SQL Server 2014
  Este tópico descreve os recursos substituídos que ainda estão disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Esses recursos estão programados para serem removidos em uma versão futura do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Recursos preteridos não devem ser usados em aplicativos novos.  
  
## <a name="features-not-supported-in-the-next-version-of-includessnoversionincludesssnoversion-mdmd"></a>Recursos sem suporte na próxima versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Os recursos do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] a seguir não terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Não use esses recursos em novo trabalho de desenvolvimento e, assim que possível, modifique os aplicativos que os utilizam atualmente. A coluna Nome do recurso aparece em eventos de rastreamento como ObjectName, em contadores de desempenho e sys.dm_os_performance_counters como nome_da_instância. O ID do Recurso aparece em eventos de rastreamento como ObjectId.  
  
|Categoria|Recurso substituído|Substituição|Nome do recurso|ID do Recurso|  
|--------------|------------------------|-----------------|------------------|----------------|  
|Programação de Dados|[sys. soap_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) ou ASP.NET|Serviços Web XML nativos|22|  
|Programação de Dados|[sys. endpoint_webmethods &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) ou ASP.NET|Serviços Web XML nativos|23|  
  
### <a name="slipstream-functionality"></a>Funcionalidade de instalação integrada  
 O [recurso de atualização de produto](/previous-versions/sql/sql-server-2012/hh231670(v=sql.110)?redirectedfrom=MSDN) foi introduzido no SQL Server 2012 como uma extensão para a funcionalidade de slipstream que [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] estava disponível no PCU1. No SQL Server 2014, o recurso de atualização do produto é o método recomendado para a correção de SQL Server. Portanto, os parâmetros de linha de comando,/*PCUSource* e/*CUSource*, associados à funcionalidade de slipstream original, não devem mais ser usados. Esses parâmetros continuarão a funcionar, mas poderão ser removidos em uma versão futura da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instalação. O parâmetro recomendado a ser usado é/*updatename* que combina a funcionalidade dos parâmetros de slipstream originais,/*PCUSource* e/*CUSource*.  
  
 Para obter mais informações sobre a funcionalidade de slipstream que [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] estava disponível no PCU1, consulte [slipstream a SQL Server Update](https://go.microsoft.com/fwlink/?LinkId=219945) (https://go.microsoft.com/fwlink/?LinkId=219945).  
 Para obter informações sobre como usar/*atualizname* para corrigir SQL Server builds, consulte o seguinte:
 
 - [Como corrigir a instalação do SQL Server 2012 com um pacote de instalação atualizado (usando o updatename para obter uma configuração inteligente)](https://blogs.msdn.microsoft.com/jason_howell/2012/08/28/how-to-patch-sql-server-2012-setup-with-an-updated-setup-package-using-updatesource-to-get-a-smart-setup/)
 
 - [SQL Server instalação do 2012 ficou mais inteligente...](https://techcommunity.microsoft.com/t5/SQL-Server-Support/SQL-Server-2012-Setup-just-got-smarter-8230/ba-p/317440)
 
## <a name="see-also"></a>Consulte Também  
 [Compatibilidade com versões anteriores](../../2014/getting-started/backward-compatibility.md)  
  
  
