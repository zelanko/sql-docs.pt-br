---
title: sys. firewall_rules (banco de dados SQL do Azure) | Microsoft Docs
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 91c3a4101f19afe4a986514fea8dab207c6d9b48
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70155548"
---
# <a name="sysfirewall_rules-azure-sql-database"></a>sys.firewall_rules (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre as configurações de firewall no nível de servidor associadas [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]ao seu.  
  
 A exibição `sys.firewall_rules` contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**INTEIRO**|O identificador da configuração de firewall de nível de servidor.|  
|name|**NVARCHAR (128)**|O nome escolhido para descrever e distinguir a configuração de firewall de nível de servidor.|  
|start_ip_address|**VARCHAR (45)**|O endereço IP mais baixo no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou maiores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais baixo possível é `0.0.0.0`.|  
|end_ip_address|**VARCHAR (45)**|O endereço IP mais alto no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou menores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais alto possível é `255.255.255.255`.<br /><br /> Observação: as tentativas de conexão do Azure são permitidas quando esse **start_ip_address** campo e o `0.0.0.0`campo de start_ip_address é igual a.|  
|create_date|**HORÁRIO**|A data e a hora UTC em que a configuração de firewall de nível de servidor foi criada.<br /><br /> Observação: o UTC é um acrônimo para tempo universal coordenado.|  
|modify_date|**HORÁRIO**|A data e a hora UTC em que a configuração de firewall de nível de servidor foi modificada por último.|  
  
## <a name="remarks"></a>Comentários

 Para retornar informações sobre as configurações de firewall no nível de banco de dados associadas à sua Banco de Dados SQL do Microsoft Azure, use [Sys. database_firewall_rules &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permissões

 O acesso somente leitura a essa exibição está disponível para todos os usuários com permissão para se conectar ao banco de dados **mestre** .  
  
## <a name="see-also"></a>Consulte Também

[sp_set_firewall_rule &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sp_set_database_firewall_rule &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[sys. database_firewall_rules &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
[Configurar um firewall do Windows para acesso Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[Configurar um firewall para acesso ao FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md) 
