---
title: Reciclar logs de erros do SQL Server Agent
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5c6079a5cab1972721fdac6c2d097fa6abb938ca
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247351"
---
# <a name="recycle-sql-server-agent-error-logs"></a>Reciclar logs de erros do SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use essa página para reciclar os logs de erros do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. A reciclagem do log encerra o log de erros atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e inicia um novo log de erros sem reiniciar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Observe que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém os nove logs de erros mais recentes. Se já houver nove logs de erros presentes, a reciclagem do log de erros faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent remova o log de erros mais antigo.  
  
## <a name="see-also"></a>Consulte Também  
[Log de erros do SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
