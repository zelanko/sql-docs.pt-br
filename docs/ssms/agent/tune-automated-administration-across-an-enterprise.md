---
title: Ajustar a administração automatizada em toda a empresa | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4a4623b604e052f9e98e3f1897a97afa8bedabd7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745344"
---
# <a name="tune-automated-administration-across-an-enterprise"></a>Ajustar a administração automatizada em toda a empresa
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

A administração multisservidor com o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se beneficia dos recursos de autoajuste do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, sob condições normais, não são necessários ajustes adicionais de trabalhos. No entanto, a carga da rede aumenta quando há execução de trabalhos, geração de alertas e notificação de operadores. Você pode ajustar a administração automatizada em toda a empresa para minimizar o tráfego de rede causado por essas atividades.  
  
## <a name="see-also"></a>Consulte Também  
[Monitorando o desempenho do mecanismo de fluxo de dados](../../integration-services/performance/performance-counters.md)  
  
