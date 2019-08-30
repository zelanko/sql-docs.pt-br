---
title: sp_set_firewall_rule (banco de dados SQL do Azure) | Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
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
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 9bc37626879b743eb3a5d0864490dc3543a8d8a9
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70152060"
---
# <a name="sp_set_firewall_rule-azure-sql-database"></a>sp_set_firewall_rule (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

  Cria ou atualiza as configurações de firewall em nível de servidor para seu servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Esse procedimento armazenado só está disponível no banco de dados mestre para o logon da entidade de segurança no nível do servidor ou atribuído Azure Active Directory entidade de segurança.  
  
  
## <a name="syntax"></a>Sintaxe  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 A tabela a seguir demonstra os argumentos e as opções [!INCLUDE[msCoName](../../includes/msconame-md.md)] com suporte no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
|Nome|Datatype|Descrição|  
|----------|--------------|-----------------|  
|[@name =] 'name'|**NVARCHAR(128)**|O nome usado para descrever e distinguir a configuração de firewall de nível de servidor.|  
|[@start_ip_address =] 'start_ip_address'|**VARCHAR(50)**|O endereço IP mais baixo no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou maiores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais baixo possível é `0.0.0.0`.|  
|[@end_ip_address =] 'end_ip_address'|**VARCHAR(50)**|O endereço IP mais alto no intervalo da configuração do firewall em nível de servidor. Os endereços IP iguais a ou menores que esse podem tentar se conectar ao servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais alto possível é `255.255.255.255`.<br /><br /> Observação: As tentativas de conexão do Azure são permitidas quando esse campo e o `0.0.0.0`campo start_ip_address são iguais.|  
  
## <a name="remarks"></a>Comentários  
 Os nomes das configurações de firewall de nível de servidor devem ser exclusivos. Se o nome da configuração fornecida para o procedimento armazenado já existir na tabela de configurações de firewall, os endereços IP inicial e final serão atualizados. Caso contrário, uma nova configuração de firewall de nível de servidor será criada.  
  
 Quando você adiciona uma configuração de firewall no nível de servidor em que os endereços IP inicial e final `0.0.0.0`são iguais, você habilita o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] acesso ao seu servidor do Azure. Forneça um valor para o parâmetro *Name* que ajudará você a se lembrar do que é a configuração de firewall no nível de servidor.  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissões  
 Somente o logon da entidade de segurança no nível do servidor criado pelo processo de provisionamento ou uma entidade de Azure Active Directory atribuída como administrador podem criar ou modificar regras de firewall no nível de servidor. O usuário deve estar conectado ao banco de dados mestre para executar sp_set_firewall_rule.  
  
## <a name="examples"></a>Exemplos  
 O código a seguir cria uma configuração de firewall no nível `Allow Azure` de servidor chamada que habilita o acesso do Azure. Execute o seguinte no banco de dados mestre virtual.  
  
```  
-- Enable Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 O código a seguir cria uma configuração de firewall de nível de servidor chamada `Example setting 1` somente para o endereço IP `0.0.0.2`. Em seguida, `sp_set_firewall_rule` o procedimento armazenado é chamado novamente para atualizar o endereço IP final `0.0.0.4`para, nessa configuração de firewall. Isso cria um intervalo que permite endereços `0.0.0.2`IP, `0.0.0.3`e `0.0.0.4` para acessar o servidor.  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Firewall do banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Como: Definir configurações de firewall (banco de dados SQL do Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sys. firewall_rules &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)
