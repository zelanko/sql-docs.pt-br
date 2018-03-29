---
title: Ajustar a administração automatizada em toda a empresa | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
caps.latest.revision: ''
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 73af3d205022ed27d137640d374220c3ea8c5129
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
# <a name="tune-automated-administration-across-an-enterprise"></a>Ajustar a administração automatizada em toda a empresa
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

A administração multisservidor com o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent se beneficia dos recursos de autoajuste do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Portanto, sob condições normais, não são necessários ajustes adicionais de trabalhos. No entanto, a carga da rede aumenta quando há execução de trabalhos, geração de alertas e notificação de operadores. Você pode ajustar a administração automatizada em toda a empresa para minimizar o tráfego de rede causado por essas atividades.  
  
## <a name="see-also"></a>Consulte Também  
[Monitorando o desempenho do mecanismo de fluxo de dados](http://msdn.microsoft.com/en-us/11e17f4e-72ed-44d7-a71d-a68937a78e4c)  
  
