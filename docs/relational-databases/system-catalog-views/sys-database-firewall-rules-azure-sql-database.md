---
description: sys.database_firewall_rules (Banco de Dados SQL do Azure)
title: sys.database_firewall_rules (banco de dados SQL do Azure) | Microsoft Docs
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
monikerRange: = azuresqldb-current
ms.openlocfilehash: 244c4245c81e264ea82c5434f8788b3960700641
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475207"
---
# <a name="sysdatabase_firewall_rules-azure-sql-database"></a>sys.database_firewall_rules (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Retorna informações sobre as configurações de firewall no nível de banco de dados associadas ao seu [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] . As configurações de firewall no nível de banco de dados são particularmente úteis ao usar usuários do banco de dados independente. Para obter mais informações, consulte [Usuários do banco de dados independente – Tornando o banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
 A exibição `sys.database_firewall_rules` contém as seguintes colunas:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**INTEGER**|O identificador da configuração de firewall de nível de banco de dados.|  
|name|**NVARCHAR (128)**|O nome escolhido para descrever e distinguir a configuração de firewall de nível de banco de dados.|  
|start_ip_address|**VARCHAR (45)**|O endereço IP mais baixo no intervalo da configuração do firewall em nível de banco de dados. Os endereços IP iguais a ou maiores que esse podem tentar se conectar à instância do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais baixo possível é `0.0.0.0`.|  
|end_ip_address|**VARCHAR (45)**|O endereço IP mais alto no intervalo da configuração do firewall. Os endereços IP iguais a ou menores que esse podem tentar se conectar à instância do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais alto possível é `255.255.255.255`.<br /><br /> Observação: as tentativas de conexão do Azure são permitidas quando esse campo e o campo de **start_ip_address** é igual a `0.0.0.0` .|  
|create_date|**HORÁRIO**|A data e a hora UTC em que a configuração de firewall de nível de banco de dados foi criada.|  
|modify_date|**HORÁRIO**|A data e a hora UTC em que a configuração de firewall de nível de banco de dados foi modificada por último.|  
  
## <a name="remarks"></a>Comentários  
 Para retornar informações sobre as configurações de firewall no nível de servidor associadas à sua Banco de Dados SQL do Microsoft Azure, use [Sys.firewall_rules (banco de dados SQL do Azure)](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md).  
  
## <a name="permissions"></a>Permissões  
 Essa exibição está disponível no banco de dados **mestre** e em cada banco de dados de usuário. O acesso somente leitura a essa exibição está disponível para todos os usuários com permissão para se conectar ao banco de dados.  
  
## <a name="see-also"></a>Consulte Também
[sp_set_database_firewall_rule &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)  
[sp_delete_database_firewall_rule &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)  
[sp_set_firewall_rule &#40;Banco de Dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)  
[sp_delete_firewall_rule &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-firewall-rule-azure-sql-database.md)   
[sys.firewall_rules &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
[Configurar um firewall do Windows para acesso Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)     
[Configurar um firewall para acesso ao FILESTREAM](../../relational-databases/blob/configure-a-firewall-for-filestream-access.md)  
[Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
