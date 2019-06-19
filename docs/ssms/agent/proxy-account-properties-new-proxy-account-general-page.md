---
title: Propriedades de conta proxy – Nova conta proxy (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.proxy.general.f1
ms.assetid: 5cd81265-bf59-413b-8397-150ddc70d0c7
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 072910b06ed75a5aad53bb6f51f0d62224144459
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65088772"
---
# <a name="proxy-account-properties---new-proxy-account-general-page"></a>Propriedades de conta proxy – Conta proxy nova (página Geral)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use essa página para exibir ou alterar as propriedades de uma conta proxy do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Nome do proxy**  
Digite o nome do proxy.  
  
**Nome da credencial**  
Digite o nome da credencial para o proxy.  
  
> [!NOTE]  
> O nome da credencial fornecido deve ser o nome de uma credencial existente. Para obter informações sobre como criar credenciais, veja [Como criar um proxy (SQL Server Management Studio)](https://msdn.microsoft.com/c1e77e91-2a69-40d9-b8b3-97cffc710586)  
  
**...**  
Inicia a caixa de diálogo **Selecionar Credencial** .  
  
**Descrição**  
Digite a descrição para o proxy.  
  
**Ativo nos seguintes subsistemas**  
Selecione os subsistemas para os quais a conta proxy tem acesso.  
  
**Reatribuir etapas de trabalho para**  
Selecione o proxy para o qual reatribuir etapas de trabalho. Essa lista está habilitada quando você revogar o acesso a um subsistema para o qual proxy tinha acesso anteriormente.  
  
## <a name="see-also"></a>Consulte Também  
[Criar um proxy do SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
