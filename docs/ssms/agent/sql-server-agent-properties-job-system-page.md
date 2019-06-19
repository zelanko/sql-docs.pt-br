---
title: Propriedades do SQL Server Agent (página Sistema de Trabalho) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a71dda192bebbe84876b2e4fbcb770f5967127c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65089610"
---
# <a name="sql-server-agent-properties-job-system-page"></a>Propriedades do SQL Server Agent (página Sistema de Trabalho)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use esta página para exibir e modificar o modo como o serviço do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent gerencia trabalhos.  
  
## <a name="options"></a>Opções  
**Intervalo de tempo limite de desligamento (em segundos)**  
Especifica o número de segundos que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent espera os trabalhos serem concluídos antes de desligar. Se o trabalho ainda estiver em execução depois do intervalo especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para o trabalho à força.  
  
**Usar uma conta proxy não administrador**  
Define uma conta proxy não administrador para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] e as versões posteriores dão suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**User name**  
Digite o nome do usuário para a conta proxy não administrador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**Senha**  
Digite a senha do usuário para a conta proxy não administrador. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e as versões posteriores dão suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent anteriores ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
**Domínio**  
Digite o domínio do usuário para a conta proxy não administrador. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a vários proxies; portanto, essa opção será aplicável somente ao gerenciar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent anteriores ao [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[Implementar trabalhos](../../ssms/agent/implement-jobs.md)  
  
