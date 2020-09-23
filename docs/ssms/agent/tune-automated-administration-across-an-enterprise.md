---
description: Ajustar a administração automatizada em toda a empresa
title: Ajustar a administração automatizada em toda a empresa
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9833b71673e20b776d1f7632090f66a174e3ed82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497472"
---
# <a name="tune-automated-administration-across-an-enterprise"></a>Ajustar a administração automatizada em toda a empresa

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> Atualmente, na [Instância Gerenciada de SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.

A administração multisservidor com o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se beneficia dos recursos de autoajuste do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, sob condições normais, não são necessários ajustes adicionais de trabalhos. No entanto, a carga da rede aumenta quando há execução de trabalhos, geração de alertas e notificação de operadores. Você pode ajustar a administração automatizada em toda a empresa para minimizar o tráfego de rede causado por essas atividades.  

## <a name="see-also"></a>Consulte Também

[Monitorando o desempenho do mecanismo de fluxo de dados](../../integration-services/performance/performance-counters.md)
