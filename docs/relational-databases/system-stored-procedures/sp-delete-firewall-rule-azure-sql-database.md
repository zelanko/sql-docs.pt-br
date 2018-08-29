---
title: sp_delete_firewall_rule (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: ''
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_firewall_rule_TSQL
- sp_delete_firewall_rule
- sys.sp_delete_firewall_rule
- sys.sp_delete_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_firewall_rule procedure
ms.assetid: cf93eed1-ba97-4850-9fcc-b9c5a9317908
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f072cc411eaa54757c518b94fec93f9435ccf2c9
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033869"
---
# <a name="spdeletefirewallrule-azure-sql-database"></a>sp_delete_firewall_rule (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Remove as configurações de firewall no nível do servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Este procedimento armazenado só está disponível no banco de dados mestre para o logon principal do nível do servidor.  

  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_delete_firewall_rule [@name =] 'name' 
[ ; ] 
```  
  
## <a name="arguments"></a>Argumentos  
 O argumento do procedimento armazenado é:  
  
 [@name =] '*nome*'  
 O nome da configuração de firewall de nível de servidor que será removida. *nome da* está **nvarchar (128)** sem nenhum padrão.  
  
## <a name="remarks"></a>Remarks  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Somente o logon de entidade de segurança no nível do servidor criado pelo processo de provisionamento pode excluir as regras de firewall de nível de servidor. O usuário deve estar conectado ao banco de dados mestre para executar sp_delete_firewall_rule.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir remove a configuração de firewall de nível de servidor chamada 'Configuração de exemplo 1'. Execute a instrução no banco de dados mestre virtual.  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>Consulte também  
 [Firewall de banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Como: definir configurações de Firewall (banco de dados SQL do Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;banco de dados SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sys. firewall_rules &#40;banco de dados SQL&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
  


