---
title: sp_adddistributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistributor
- sp_adddistributor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_adddistributor
ms.assetid: 35415502-68d0-40f6-993c-180e50004f1e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 45088122cfb6824598aaf40486264d41216d3c39
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771316"
---
# <a name="spadddistributor-transact-sql"></a>sp_adddistributor (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cria uma entrada na tabela [Sys. sysservers](../../relational-databases/system-compatibility-views/sys-sysservers-transact-sql.md) (se não houver uma), marca a entrada do servidor como um distribuidor e armazena informações de propriedade. Esse procedimento armazenado é executado no Distribuidor, no banco de dados mestre, para registrar e marcar o servidor como Distribuidor. No caso de um Distribuidor remoto, é também executado no Publicador do banco de dados mestre para registrar o distribuidor remoto.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_adddistributor [ @distributor= ] 'distributor'   
    [ , [ @heartbeat_interval= ] heartbeat_interval ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @from_scripting= ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @distributor = ] 'distributor'`É o nome do servidor de distribuição. o *distribuidor* é **sysname**, sem padrão. Esse parâmetro só é usado na configuração de um Distribuidor remoto. Ele adiciona entradas para as propriedades do distribuidor no **msdb.. Tabela MSdistributor** .  
  
`[ @heartbeat_interval = ] heartbeat_interval`É o número máximo de minutos que um agente pode acessar sem registrar uma mensagem de progresso. *heartbeat_interval* é **int**, com um padrão de 10 minutos. Um trabalho do SQL Server Agent é criado e executado nesse intervalo para verificar os status dos agentes de replicação em execução.  
  
`[ @password = ] 'password']`É a senha do logon do **distributor_admin** . a *senha* é **sysname**, com um padrão de NULL. Se for NULL ou uma cadeia de caracteres vazia, a senha será reajustada a um valor aleatório. A senha deve ser configurada quando o primeiro distribuidor remoto é adicionado. o logon e a *senha* do **distributor_admin** são armazenados para a entrada de servidor vinculada usada para uma conexão RPC do *distribuidor* , incluindo conexões locais. Se o *distribuidor* for local, a senha de **distributor_admin** será definida como um novo valor. Para Publicadores com um distribuidor remoto, o mesmo valor para *senha* deve ser especificado ao executar **sp_adddistributor** no Publicador e no distribuidor. [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) pode ser usado para alterar a senha do distribuidor.  
  
> [!IMPORTANT]  
>  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_adddistributor** é usado na replicação de instantâneo, na replicação transacional e na replicação de mesclagem.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistributor-transa_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_adddistributor**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributor_property &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md)   
 [sp_dropdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributor-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)  
  
  
