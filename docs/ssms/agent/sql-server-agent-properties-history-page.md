---
title: Propriedades do SQL Server Agent (página Histórico) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 5e61393109ef05efbe1941d6a5bb56164928c8a7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632074"
---
# <a name="sql-server-agent-properties-history-page"></a>Propriedades do SQL Server Agent (página Histórico)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use essa página para exibir e modificar as configurações de gerenciamento do log de histórico do serviço [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Limitar tamanho do log do histórico de trabalho**  
Define limites para a quantidade de informações do histórico de trabalho que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém no log.  
  
**Tamanho máximo (em linhas) do log do histórico de trabalho**  
Define o número máximo de linhas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém. Quando o log aumenta para conter esse número de linhas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent remove as linhas mais antigas do log à medida que novas linhas forem inseridas.  
  
**Máximo de linhas do histórico de trabalho por trabalho**  
Define o número máximo de linhas que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantém por trabalho. Quando o log de um determinado trabalho cresce até conter esse número de linhas, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent remove as linhas mais antigas do log à medida que novas linhas são inseridas.  
  
**Remover histórico de agente**  
Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent removerá as entradas presentes no log por mais tempo do que o período especificado. Essa é uma execução de uma vez para remover o histórico. Se um trabalho recorrente for necessário, crie e agende um plano de manutenção com um trabalho de limpeza.  
  
**Com mais de**  
Define o período durante o qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent manterá entradas.  
  
## <a name="see-also"></a>Consulte Também  
[Log de erros do SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
