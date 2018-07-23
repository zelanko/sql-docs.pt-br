---
title: Propriedades do SQL Server Agent (página Conexão) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.connection.f1
ms.assetid: d6a677ff-60ad-47ba-a0cb-df4193b165e0
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 37afadef09a3b971977247c0311d3d63a4dae020
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37983852"
---
# <a name="sql-server-agent-properties-connection-page"></a>Propriedades do SQL Server Agent (página Conexão)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use esta página para exibir e modificar as configurações da conexão do serviço [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="options"></a>Opções  
**Servidor de host local do alias**  
Especifica o alias a ser usado para se conectar à instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Se você não puder usar as opções de conexão padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, defina um alias para a instância e especifique o alias aqui.  
  
**Usar Autenticação do Windows**  
Define a autenticação do [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows como o método de autenticação usado para conectar-se com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent conecta-se como a conta com que o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é executado.  
  
**Usar Autenticação do SQL Server**  
Define a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como o método de autenticação usado para conectar-se com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] A autenticação é fornecida para fins de compatibilidade com versões anteriores. Para maior segurança, use a autenticação do Windows, se possível.  
  
**Logon**  
Especifica o nome de logon a ser usado para conectar-se com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Senha**  
Especifica a senha a ser usada para conectar-se com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
