---
title: sp_delete_database_firewall_rule (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_database_firewall_rule
- sp_delete_database_firewall_rule_TSQL
- sys.sp_delete_database_firewall_rule
- sys.sp_delete_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_database_firewall_rule procedure
ms.assetid: ed295312-e586-4fc2-9e80-806b490ee7bd
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 88aeeff5d675584adfa22fbd0d5c0f479fc1d9ce
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="spdeletedatabasefirewallrule-azure-sql-database"></a>sp_delete_database_firewall_rule (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Remove a configuração de firewall no nível de banco de dados da sua [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Regras de firewall do banco de dados podem ser configuradas e excluídas do banco de dados mestre e para bancos de dados do usuário em [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].   
  
 
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_database_firewall_rule [@name =] [N]'name'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@name =**] **'***nome***'**  
 O nome da configuração de firewall de nível de banco de dados que será removida. *nome* é **nvarchar (128)** sem nenhum valor padrão. O identificador de Unicode `N` é opcional para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. 
  
## <a name="permissions"></a>Permissões  
 Somente o nível de servidor principal logon criado pelo processo de provisionamento ou uma entidade de segurança do Active Directory do Azure atribuída como o administrador pode excluir regras de firewall de nível de banco de dados.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir remove o nível de banco de dados de configuração de firewall denominada `Example DB Setting 1`.
  
```  
-- Remove database-level firewall setting  
EXECUTE sp_delete_database_firewall_rule N'Example DB Setting 1';  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Firewall de banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Como: definir configurações de Firewall (banco de dados do SQL Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_set_database_firewall_rule &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md)   
 [sys. database_firewall_rules &#40;banco de dados do SQL Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  


