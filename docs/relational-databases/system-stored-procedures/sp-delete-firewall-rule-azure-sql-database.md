---
description: sp_delete_firewall_rule (Banco de Dados SQL do Azure)
title: sp_delete_firewall_rule
titleSuffix: Azure SQL Database
ms.date: 07/27/2016
ms.service: sql-database
ms.reviewer: ''
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
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest
ms.openlocfilehash: 22edbde7dacf45c670c94d77e7cf48833445c346
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472697"
---
# <a name="sp_delete_firewall_rule-azure-sql-database"></a>sp_delete_firewall_rule (Banco de Dados SQL do Azure)
[!INCLUDE [asdb-asa](../../includes/applies-to-version/asdb-asa.md)]

  Remove as configurações de firewall no nível do servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Este procedimento armazenado só está disponível no banco de dados mestre para o logon principal do nível do servidor.  

  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_delete_firewall_rule [@name =] 'name' 
[ ; ] 
```  
  
## <a name="arguments"></a>Argumentos  
 O argumento do procedimento armazenado é:  
  
 [ @name =] '*nome*'  
 O nome da configuração de firewall de nível de servidor que será removida. *nome* é **nvarchar (128)** sem padrão.  
  
## <a name="remarks"></a>Comentários  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Somente o logon de entidade de segurança no nível do servidor criado pelo processo de provisionamento pode excluir as regras de firewall de nível de servidor. O usuário deve estar conectado ao banco de dados mestre para executar sp_delete_firewall_rule.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir remove a configuração de firewall de nível de servidor chamada 'Configuração de exemplo 1'. Execute a instrução no banco de dados mestre virtual.  
  
```   
EXEC sp_delete_firewall_rule N'Example setting 1';   
```  
  
## <a name="see-also"></a>Consulte Também  
 [Firewall do banco de dados SQL do Azure](/azure/azure-sql/database/firewall-configure)   
 [Como: definir configurações de firewall (banco de dados SQL do Azure)](/azure/azure-sql/database/firewall-configure)   
 [sp_set_firewall_rule &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sys.firewall_rules &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)  
  
