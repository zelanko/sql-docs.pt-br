---
description: Propriedades de conta proxy – Conta proxy nova (página Geral)
title: Propriedades de conta proxy – Conta proxy nova (página Geral)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.proxy.general.f1
ms.assetid: 5cd81265-bf59-413b-8397-150ddc70d0c7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a70ba36150771ef90f3cfc9461c018c212da4c73
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037287"
---
# <a name="proxy-account-properties---new-proxy-account-general-page"></a>Propriedades de conta proxy – Conta proxy nova (página Geral)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> Atualmente, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.

Use essa página para exibir ou alterar as propriedades de uma conta proxy do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Nome do proxy**  
Digite o nome do proxy.  
  
**Nome da credencial**  
Digite o nome da credencial para o proxy.  
  
> [!NOTE]  
> O nome da credencial fornecido deve ser o nome de uma credencial existente. Para obter informações sobre como criar credenciais, veja [Como Criar um proxy](../../relational-databases/security/authentication-access/create-a-credential.md)  
  
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
