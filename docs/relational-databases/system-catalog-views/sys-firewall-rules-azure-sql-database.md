---
title: sys. firewall_rules (banco de dados SQL) | Microsoft Docs
ms.date: 03/26/2019
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.firewall_rules
- firewall_rules
- sys.firewall_rules_TSQL
- firewall_rules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- firewall_rules
- sys.firewall_rules
ms.assetid: 140d2cd8-9aa1-4cc5-870d-e1dbc873b3fe
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5127dacf628231199c5ce5ac49fdb2377c82f270
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62631596"
---
# <a name="sysfirewallrules-azure-sql-database"></a>sys.firewall_rules (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre as configurações de firewall de nível de servidor associado com seu [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 A exibição `sys.firewall_rules` contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**INT**|O identificador da configuração de firewall de nível de servidor.|  
|nome|**NVARCHAR(128)**|O nome escolhido para descrever e distinguir a configuração de firewall de nível de servidor.|  
|start_ip_address|**VARCHAR(45)**|O endereço IP mais baixo no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou maiores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais baixo possível é `0.0.0.0`.|  
|end_ip_address|**VARCHAR(45)**|O endereço IP mais alto no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou menores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais alto possível é `255.255.255.255`.<br /><br /> Observação: Tentativas de conexão do Windows Azure são permitidas quando esse campo e o **start_ip_address** campo equals `0.0.0.0`.|  
|create_date|**DATETIME**|A data e a hora UTC em que a configuração de firewall de nível de servidor foi criada.<br /><br /> Observação: UTC é um acrônimo para o tempo Universal Coordenado.|  
|modify_date|**DATETIME**|A data e a hora UTC em que a configuração de firewall de nível de servidor foi modificada por último.|  
  
## <a name="remarks"></a>Comentários

 Para retorna informações sobre as configurações de firewall de nível de banco de dados associado com o Microsoft Azure SQL Database, use [sys. database_firewall_rules &#40;banco de dados SQL&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permissões

 Acesso somente leitura a essa exibição está disponível para todos os usuários com permissão para conexão com o **mestre** banco de dados.  
  
## <a name="see-also"></a>Consulte também

[sp_set_firewall_rule &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;banco de dados SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;banco de dados SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[sys. database_firewall_rules &#40;banco de dados SQL&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[Configurar um Firewall do Windows para acesso ao mecanismo de banco de dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[Configurar um firewall para acesso ao FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
