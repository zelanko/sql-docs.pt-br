---
title: sp_set_firewall_rule (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
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
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e9315c7ca138d352ee9f0cdffca9abe3a2242dc0
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38056104"
---
# <a name="spsetfirewallrule-azure-sql-database"></a>sp_set_firewall_rule (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Cria ou atualiza as configurações de firewall em nível de servidor para seu servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Esse procedimento armazenado só está disponível no banco de dados mestre para o logon principal no nível do servidor ou entidade de segurança do Active Directory do Azure atribuída.  
  
  
## <a name="syntax"></a>Sintaxe  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 A tabela a seguir demonstra os argumentos com suporte e as opções na [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|Nome|Datatype|Description|  
|----------|--------------|-----------------|  
|[@name =] 'name'|**NVARCHAR (128)**|O nome usado para descrever e distinguir a configuração de firewall de nível de servidor.|  
|[@start_ip_address =] 'start_ip_address'|**VARCHAR (50)**|O endereço IP mais baixo no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou maiores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais baixo possível é `0.0.0.0`.|  
|[@end_ip_address =] 'end_ip_address'|**VARCHAR (50)**|O endereço IP mais alto no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou menores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais alto possível é `255.255.255.255`.<br /><br /> Observação: Tentativas de conexão do Azure são permitidas quando esse campo e o *start_ip_address* campo equals `0.0.0.0`.|  
  
## <a name="remarks"></a>Remarks  
 Os nomes das configurações de firewall de nível de servidor devem ser exclusivos. Se o nome da configuração fornecida para o procedimento armazenado já existir na tabela de configurações de firewall, os endereços IP inicial e final serão atualizados. Caso contrário, uma nova configuração de firewall de nível de servidor será criada.  
  
 Quando você adiciona uma configuração de firewall de nível de servidor em que o início e término endereços IP são iguais a `0.0.0.0`, você habilita o acesso ao seu [!INCLUDE[ssSDS](../../includes/sssds-md.md)] server do Azure. Forneça um valor para o *nome* parâmetro que o ajudará a se lembrar de qual é a configuração de firewall no nível de servidor para.  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Somente o logon principal do nível do servidor criado pelo processo de provisionamento ou uma entidade de segurança do Azure Active Directory atribuído como o administrador pode criar ou modificar as regras de firewall no nível de servidor. O usuário deve estar conectado ao banco de dados mestre para executar sp_set_firewall_rule.  
  
## <a name="examples"></a>Exemplos  
 O código a seguir cria um firewall de nível de servidor chamada `Allow Azure` que habilita o acesso do Azure. Execute o seguinte no banco de dados mestre virtual.  
  
```  
-- Enable Windows Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 O código a seguir cria uma configuração de firewall de nível de servidor chamada `Example setting 1` somente para o endereço IP `0.0.0.2`. Em seguida, o `sp_set_firewall_rule` procedimento armazenado é chamado novamente para atualizar o endereço IP final `0.0.0.4`, nessa configuração de firewall. Isso cria um intervalo que permite que endereços IP `0.0.0.2`, `0.0.0.3`, e `0.0.0.4` para acessar o servidor.  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Firewall de banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Como: definir configurações de Firewall (banco de dados SQL do Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sys. firewall_rules &#40;banco de dados SQL&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
