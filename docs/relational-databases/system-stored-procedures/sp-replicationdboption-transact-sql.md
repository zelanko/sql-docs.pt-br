---
title: sp_replicationdboption (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_replicationdboption_TSQL
- sp_replicationdboption
helpviewer_keywords: sp_replicationdboption
ms.assetid: d021864e-3f21-4d1a-89df-6c1086f753bf
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 584c9ed9f4a9d0e00bcbd0de05788a1841189899
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spreplicationdboption-transact-sql"></a>sp_replicationdboption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define uma opção de banco de dados de replicação para o banco de dados especificado. Esse procedimento armazenado é executado no Publicador ou no Assinante, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replicationdboption [ @dbname= ] 'db_name'   
        , [ @optname= ] 'optname'   
        , [ @value= ] 'value'   
    [ , [ @ignore_distributor= ] ignore_distributor ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [**@dbname=**] **'***dbname***'**  
 É o banco de dados para o qual a opção de banco de dados de replicação está sendo definida. *DB_NAME* é **sysname**, sem padrão.  
  
 [**@optname=**] **'***optname***'**  
 É a opção de banco de dados de replicação a ser habilitada ou desabilitada. *optname* é **sysname**, e pode ser um destes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**publicação de mesclagem**|O banco de dados pode ser usado para publicações de mesclagem.|  
|**Publicar**|O banco de dados pode ser usado para outros tipos de publicação.|  
|**Inscrever-se**|O banco de dados é um banco de dados de assinatura.|  
|**sincronizar com backup**|O banco de dados está habilitado para backup coordenado. Para obter mais informações, consulte [habilitar Backups coordenados para replicação transacional &#40; Programação Transact-SQL &#41; ](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md).|  
  
 [  **@value=**] **'***valor***'**  
 Especifica se a opção de banco de dados de replicação deve ser habilitada ou desabilitada. *valor* é **sysname**e pode ser **true** ou **false**. Quando esse valor é **false** e *optname* é **publicação de mesclagem**, assinaturas para o banco de dados publicado de mesclagem também serão removidas.  
  
 [  **@ignore_distributor=**] *ignore_distributor*  
 Indica se esse procedimento armazenado será executado sem se conectar ao Distribuidor. *ignore_distributor* é **bit**, com um padrão de **0**, significando que o distribuidor deve ser conectado ao e atualizado com o novo status do banco de dados de publicação. O valor **1** só deve ser especificado se o distribuidor estiver inacessível e **sp_replicationdboption** está sendo usado para desabilitar a publicação.  
  
 [  **@from_scripting=**] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replicationdboption** é usado em replicação de instantâneo, replicação transacional e replicação de mesclagem.  
  
 Esse procedimento cria ou descarta tabelas do sistema de replicação específicas, contas de segurança, e assim por diante, que depende das opções fornecidas. Define a categoria correspondente bit no **sysdatabases** tabela do sistema e cria as tabelas de sistema necessários.  
  
 Para desabilitar a publicação, o banco de dados de publicação deve estar online. Se um instantâneo do banco de dados existir para o banco de dados de publicação, deverá ser descartado antes de desabilitar a publicação. O instantâneo do banco de dados é uma cópia offline somente leitura de um banco de dados e não está relacionado a um instantâneo de replicação. Para obter mais informações, consulte [Instantâneos de banco de dados &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** pode executar a função de servidor fixa **sp_replicationdboption**.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Criar uma publicação](../../relational-databases/replication/publish/create-a-publication.md)   
 [Excluir uma publicação](../../relational-databases/replication/publish/delete-a-publication.md)   
 [Desabilitar a publicação e a distribuição](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [sysdatabases &#40; Transact-SQL &#41;](../../relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
