---
title: sys. database_firewall_rules (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-database
ms.reviewer: ''
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
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 61402b762b7a6b4d944214d59e187e1457e93f93
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155764"
---
# <a name="sysdatabase_firewall_rules-azure-sql-database"></a>sys.database_firewall_rules (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre as configurações de firewall no nível de banco de [!INCLUDE[msCoName](../../includes/msconame-md.md)] dados associadas ao seu [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. As configurações de firewall no nível de banco de dados são particularmente úteis ao usar usuários do banco de dados independente. Para obter mais informações, consulte [Usuários de bancos de dados independentes – Tornando seu banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
 A exibição `sys.database_firewall_rules` contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**INTEGER**|O identificador da configuração de firewall de nível de banco de dados.|  
|name|**NVARCHAR(128)**|O nome escolhido para descrever e distinguir a configuração de firewall de nível de banco de dados.|  
|start_ip_address|**VARCHAR(45)**|O endereço IP mais baixo no intervalo da configuração do firewall em nível de banco de dados. Os endereços IP iguais a ou maiores que esse podem tentar se conectar à instância do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais baixo possível é `0.0.0.0`.|  
|end_ip_address|**VARCHAR(45)**|O endereço IP mais alto no intervalo da configuração do firewall. Os endereços IP iguais a ou menores que esse podem tentar se conectar à instância do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais alto possível é `255.255.255.255`.<br /><br /> Observação: As tentativas de conexão do Azure são permitidas quando esse campo e o `0.0.0.0`campo start_ip_address são iguais.|  
|create_date|**DATETIME**|A data e a hora UTC em que a configuração de firewall de nível de banco de dados foi criada.|  
|modify_date|**DATETIME**|A data e a hora UTC em que a configuração de firewall de nível de banco de dados foi modificada por último.|  
  
## <a name="remarks"></a>Comentários  
 Para retornar informações sobre as configurações de firewall no nível de servidor associadas à sua Banco de Dados SQL do Microsoft Azure, use [Sys. firewall_rules (banco de dados SQL do Azure)](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível no banco de dados **mestre** e em cada banco de dados de usuário. O acesso somente leitura a essa exibição está disponível para todos os usuários com permissão para se conectar ao banco de dados.  
  
## <a name="see-also"></a>Consulte também
[sp_set_database_firewall_rule &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[Banco &#40;de dados SQL do sp_delete_database_firewall_rule do Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[sp_set_firewall_rule &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[Banco &#40;de dados SQL do sp_delete_firewall_rule do Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sys. firewall_rules &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
[Configurar um firewall do Windows para acesso Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[Configurar um firewall para acesso ao FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
