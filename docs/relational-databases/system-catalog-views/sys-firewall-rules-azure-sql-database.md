---
title: sys. firewall_rules (banco de dados SQL) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
ms.openlocfilehash: 37313fc7aa6bfe29622bb6ec6900120a89e68dff
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43820522"
---
# <a name="sysfirewallrules-azure-sql-database"></a>sys.firewall_rules (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre as configurações de firewall de nível de servidor associado com seu [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 A exibição `sys.firewall_rules` contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|id|**INT**|O identificador da configuração de firewall de nível de servidor.|  
|nome|**NVARCHAR (128)**|O nome escolhido para descrever e distinguir a configuração de firewall de nível de servidor.|  
|start_ip_address|**VARCHAR (50)**|O endereço IP mais baixo no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou maiores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais baixo possível é `0.0.0.0`.|  
|end_ip_address|**VARCHAR (50)**|O endereço IP mais alto no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou menores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais alto possível é `255.255.255.255`.<br /><br /> Observação: Tentativas de conexão do Azure do Windows são permitidas quando esse campo e o **start_ip_address** campo equals `0.0.0.0`.|  
|create_date|**DATETIME**|A data e a hora UTC em que a configuração de firewall de nível de servidor foi criada.<br /><br /> Observação: UTC é um acrônimo para o tempo Universal Coordenado.|  
|modify_date|**DATETIME**|A data e a hora UTC em que a configuração de firewall de nível de servidor foi modificada por último.|  
  
## <a name="remarks"></a>Remarks  
 Para remover uma regra de firewall de banco de dados, use [sp_delete_firewall_rule &#40;banco de dados SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md). Para definir uma regra de firewall para um banco de dados, consulte [sys. database_firewall_rules &#40;banco de dados SQL&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md). Para retornar informações sobre regras de firewall existentes, consulte sys. firewall_rules (banco de dados do SQL Azure).  
  
## <a name="permissions"></a>Permissões  
 Acesso somente leitura a essa exibição está disponível para todos os usuários com permissão para conexão com o **mestre** banco de dados.  
  
## <a name="see-also"></a>Consulte também  
 [sys. database_firewall_rules &#40;banco de dados SQL&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)   
 [sp_set_firewall_rule &#40;banco de dados SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [Configurar um Firewall do Windows para acesso ao mecanismo de banco de dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [Configurar um Firewall para acesso FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)   
 [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [Como: definir as configurações do Firewall (Banco de Dados SQL do Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)  
  
  
