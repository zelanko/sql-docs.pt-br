---
title: sp_set_firewall_rule (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: 
ms.date: 07/28/2016
ms.prod: 
ms.prod_service: sql-database, sql-data-warehouse
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 38ef5788aba91bfde21df091321a69dbacbeb8e9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spsetfirewallrule-azure-sql-database"></a>sp_set_firewall_rule (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Cria ou atualiza as configurações de firewall em nível de servidor para seu servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Esse procedimento armazenado só está disponível no banco de dados mestre para o logon principal no nível de servidor ou entidade de segurança do Active Directory do Azure atribuída.  
  
  
## <a name="syntax"></a>Sintaxe  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 A tabela a seguir demonstra os argumentos com suporte e as opções em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|Nome|Datatype|Description|  
|----------|--------------|-----------------|  
|[@name =] 'name'|**NVARCHAR (128)**|O nome usado para descrever e distinguir a configuração de firewall de nível de servidor.|  
|[@start_ip_address =] 'start_ip_address'|**VARCHAR (50)**|O endereço IP mais baixo no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou maiores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais baixo possível é `0.0.0.0`.|  
|[@end_ip_address =] 'end_ip_address'|**VARCHAR (50)**|O endereço IP mais alto no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou menores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais alto possível é `255.255.255.255`.<br /><br /> Observação: As tentativas de conexão do Azure são permitidas quando esse campo e o *start_ip_address* campo é igual a `0.0.0.0`.|  
  
## <a name="remarks"></a>Comentários  
 Os nomes das configurações de firewall de nível de servidor devem ser exclusivos. Se o nome da configuração fornecida para o procedimento armazenado já existir na tabela de configurações de firewall, os endereços IP inicial e final serão atualizados. Caso contrário, uma nova configuração de firewall de nível de servidor será criada.  
  
 Quando você adiciona uma configuração de firewall de nível de servidor em que o início e término endereços IP são iguais a `0.0.0.0`, habilitar o acesso ao seu [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor do Azure. Forneça um valor para o *nome* parâmetro que ajudará você a lembrar qual é a configuração de firewall no nível de servidor para.  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessárias para autenticar uma conexão e as regras de firewall de nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e certifique-se de que um banco de dados tem a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Somente o logon principal do nível do servidor criado pelo processo de provisionamento ou uma entidade de segurança do Active Directory do Azure atribuída como o administrador pode criar ou modificar as regras de firewall de nível de servidor. O usuário deve estar conectado ao banco de dados mestre para executar sp_set_firewall_rule.  
  
## <a name="examples"></a>Exemplos  
 O código a seguir cria um nível de servidor de configuração de firewall chamada `Allow Azure` que permite o acesso do Azure. Execute o seguinte no banco de dados mestre virtual.  
  
```  
-- Enable Windows Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 O código a seguir cria uma configuração de firewall de nível de servidor chamada `Example setting 1` somente para o endereço IP `0.0.0.2`. Em seguida, o `sp_set_firewall_rule` procedimento armazenado é chamado novamente para atualizar o endereço IP final `0.0.0.4`, nessa configuração de firewall. Isso cria um intervalo que permite que os endereços IP `0.0.0.2`, `0.0.0.3`, e `0.0.0.4` para acessar o servidor.  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Firewall de banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Como: definir configurações de Firewall (banco de dados do SQL Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sys. firewall_rules &#40; Banco de dados SQL do Azure &#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
