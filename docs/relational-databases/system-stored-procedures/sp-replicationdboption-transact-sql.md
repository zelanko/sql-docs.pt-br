---
title: sp_replicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords:
- sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b45da78b0a79130cbbbd6c39bee07f237de2ef89
ms.sourcegitcommit: dacf6c57f6a2e3cf2005f3268116f3c609639905
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2019
ms.locfileid: "70878731"
---
# <a name="sp_replicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Define uma opção de banco de dados de replicação para o banco de dados especificado. Esse procedimento armazenado é executado no Publicador ou no Assinante, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replicationdboption [ @dbname= ] 'db_name'   
        , [ @optname= ] 'optname'   
        , [ @value= ] 'value'   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@dbname=** ] **'***dbname***'**  
 É o banco de dados para o qual a opção de banco de dados de replicação está sendo definida. *db_name* é **sysname**, sem padrão.  
  
 **[@optname=** ] **'***OptName***'**  
 É a opção de banco de dados de replicação a ser habilitada ou desabilitada. *OptName* é **sysname**e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**publicação de mesclagem**|O banco de dados pode ser usado para publicações de mesclagem.|  
|**publicou**|O banco de dados pode ser usado para outros tipos de publicação.|  
|**Faça**|O banco de dados é um banco de dados de assinatura.|  
|**sincronizar com backup**|O banco de dados está habilitado para backup coordenado. Para obter mais informações, consulte [habilitar backups coordenados para programação &#40;&#41;Transact-SQL de replicação de replicação transacional](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md).|  
  
`[ @value = ] 'value'`É habilitar ou desabilitar a opção de banco de dados de replicação fornecida. o *valor* é **sysname**e pode ser **true** ou **false**. Quando esse valor é **false** e *OptName* é **publicação de mesclagem**, as assinaturas para o banco de dados publicado de mesclagem também são descartadas.  
  
`[ @ignore_distributor = ] ignore_distributor`Indica se este procedimento armazenado é executado sem se conectar ao distribuidor. *ignore_distributor* é **bit**, com um padrão de **0**, o que significa que o distribuidor deve estar conectado e atualizado com o novo status do banco de dados de publicação. O valor **1** deve ser especificado somente se o distribuidor estiver inacessível e **sp_replicationdboption** estiver sendo usado para desabilitar a publicação.  
  
`[ @from_scripting = ] from_scripting` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replicationdboption** é usado na replicação de instantâneo, na replicação transacional e na replicação de mesclagem.  
  
 Esse procedimento cria ou descarta tabelas do sistema de replicação específicas, contas de segurança, e assim por diante, que depende das opções fornecidas. Define o **is_published** (replicação de transacational ou instantâneo) correspondente, o **is_merge_published** (replicação de mesclagem) ou os bits de **is_distributor** na tabela **mestre. bancos de dados** do sistema e cria o sistema necessário tabelas.  
  
 Para desabilitar a publicação, o banco de dados de publicação deve estar online. Se um instantâneo do banco de dados existir para o banco de dados de publicação, deverá ser descartado antes de desabilitar a publicação. O instantâneo do banco de dados é uma cópia offline somente leitura de um banco de dados e não está relacionado a um instantâneo de replicação. Para obter mais informações, consulte [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_replicationdboption**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Excluir uma publicação](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
