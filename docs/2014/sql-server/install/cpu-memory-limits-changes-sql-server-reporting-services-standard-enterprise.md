---
title: Alterações nos limites de CPU e memória do SQL Server Reporting Services Standard e Enterprise | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dd553715-2b95-4119-8f58-d01de388d9ab
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5097398d50c2e3072c31724cd16e56d63f5e7676
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007221"
---
# <a name="changes-to-cpu-and-memory-limits-for-sql-server-reporting-services-standard-and-enterprise"></a>Alterações nos limites de CPU e de memória para o SQL Server Reporting Services Standard e Enterprise
  O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Reporting Services edição Standard e Enterprise oferece suporte a no máximo 64 gigabytes de memória do sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
### <a name="description"></a>Description  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services edição Standard e Enterprise oferece suporte a no máximo 64 gigabytes de memória do sistema. Talvez seja necessário reconfigurar os parâmetros atuais do sistema para alinhá-los aos novos limites.  
  
 Para obter mais informações sobre os limites de CPU e memória de outras edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Compute Capacity Limits by Edition of SQL Server](../compute-capacity-limits-by-edition-of-sql-server.md), e [suporte de memória pelas edições do SQL Server](http://go.microsoft.com/fwlink/?LinkId=212633).  
  
## <a name="corrective-action"></a>Ação corretiva  
 Talvez seja necessário reconfigurar os parâmetros atuais do sistema para alinhá-los aos novos limites de CPU e memória. Para obter mais informações, consulte [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql), e [opções Server Memory de configuração de servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos com suporte nas edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Compatibilidade com versões anteriores](../../../2014/getting-started/backward-compatibility.md)  
  
  
