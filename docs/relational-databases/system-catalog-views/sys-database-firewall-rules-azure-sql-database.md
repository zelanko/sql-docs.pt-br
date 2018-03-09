---
title: sys. database_firewall_rules (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.database_firewall_rules_TSQL
- database_firewall_rules_TSQL
- sys.database_firewall_rules
- database_firewall_rules
dev_langs:
- TSQL
helpviewer_keywords:
- database_firewall_rules
- sys.database_firewall_rules
ms.assetid: 2e821593-3b9f-43d6-a99b-1ceffe177faf
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c598371c8df7a92622ec43700fc504b082640e1f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysdatabasefirewallrules-azure-sql-database"></a>sys.database_firewall_rules (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre as configurações de firewall no nível de banco de dados associadas ao seu [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. As configurações de firewall no nível de banco de dados são particularmente úteis ao usar usuários do banco de dados independente. Para obter mais informações, consulte [Usuários de bancos de dados independentes – Tornando seu banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
 A exibição `sys.database_firewall_rules` contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**NÚMERO INTEIRO**|O identificador da configuração de firewall de nível de banco de dados.|  
|name|**NVARCHAR (128)**|O nome escolhido para descrever e distinguir a configuração de firewall de nível de banco de dados.|  
|start_ip_address|**VARCHAR (50)**|O endereço IP mais baixo no intervalo da configuração do firewall em nível de banco de dados. Os endereços IP iguais a ou maiores que esse podem tentar se conectar à instância do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais baixo possível é `0.0.0.0`.|  
|end_ip_address|**VARCHAR (50)**|O endereço IP mais alto no intervalo da configuração do firewall. Os endereços IP iguais a ou menores que esse podem tentar se conectar à instância do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais alto possível é `255.255.255.255`.<br /><br /> Observação: Tentativas de conexão do Azure do Windows são permitidas quando esse campo e o **start_ip_address** campo é igual a `0.0.0.0`.|  
|create_date|**DATA E HORA**|A data e a hora UTC em que a configuração de firewall de nível de banco de dados foi criada.|  
|modify_date|**DATA E HORA**|A data e a hora UTC em que a configuração de firewall de nível de banco de dados foi modificada por último.|  
  
## <a name="remarks"></a>Comentários  
 Para remover uma regra de firewall de banco de dados, use [sp_delete_database_firewall_rule &#40; Banco de dados SQL do Azure &#41; ](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md). Para definir uma regra de firewall para todos os [!INCLUDE[ssSDS](../../includes/sssds-md.md)], consulte [sp_set_firewall_rule &#40; Banco de dados SQL do Azure &#41; ](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md). Para retornar informações sobre o banco de dados existente com as regras de firewall, consulte [sys. database_firewall_rules (banco de dados do SQL Azure)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível na **mestre** banco de dados e em cada banco de dados do usuário. O acesso somente leitura a essa exibição está disponível para todos os usuários com permissão para se conectar ao banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [sp_set_firewall_rule &#40; Banco de dados SQL do Azure &#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sys. database_firewall_rules (banco de dados do SQL Azure)](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40; Banco de dados SQL do Azure &#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [Configurar um Firewall do Windows para acesso ao mecanismo de banco de dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurar um Firewall para acesso FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
