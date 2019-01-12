---
title: sp_addmergealternatepublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergealternatepublisher_TSQL
- sp_addmergealternatepublisher
helpviewer_keywords:
- sp_addmergealternatepublisher
ms.assetid: de46e0b1-d946-4021-bff6-2d8e3187656d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 21d0ea34f3521333976ce00a3f5b823c3fcb816a
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129296"
---
# <a name="spaddmergealternatepublisher-transact-sql"></a>sp_addmergealternatepublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Permite que um Assinante use um parceiro de sincronização alternativo. As propriedades de publicação devem especificar que os Assinantes podem sincronizar com outros Publicadores. Esse procedimento armazenado é executado no assinante, no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addmergealternatepublisher [ @publisher= ] 'publisher'  
          , [ @publisher_db= ] 'publisher_db'  
          , [ @publication= ] 'publication'  
          , [ @alternate_publisher= ] 'alternate_synchronization_partner'  
          , [ @alternate_publisher_db= ] 'alternate_publisher_db'  
          , [ @alternate_publication= ] 'alternate_synchronization_partner'  
     , [ @alternate_distributor= ] 'alternate_distributor'   
    [ , [ @friendly_name= ] 'friendly_name' ]   
    [ , [ @reserved= ] 'reserved' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'**_publisher_**'**  
 É o nome do Publicador. *Publisher* está **sysname**, sem padrão.  
  
 [  **@publisher_db=**] **'**_publisher_db_**'**  
 É o nome do banco de dados de publicação. *publisher_db* está **sysname**, sem padrão.  
  
 [  **@publication=**] **'**_publicação_**'**  
 É o nome da publicação. *publicação* está **sysname**, sem padrão.  
  
 [  **@alternate_publisher=**] **'**_alternate_synchronization_partner_**'**  
 É o nome do Publicador alternativo. *alternate_synchronization_partner* está **sysname**, sem padrão.  
  
 [  **@alternate_publisher_db=**] **'**_alternate_publisher_db_**'**  
 É o nome do banco de dados da publicação no publicador alternativo. *alternate_publisher_db* está **sysname**, sem padrão.  
  
 [  **@alternate_publication=**] **'**_alternate_synchronization_partner_**'**  
 É o nome da publicação no parceiro de sincronização alternativo. *alternate_synchronization_partner* está **sysname**, sem padrão.  
  
 [  **@alternate_distributor=**] **'**_alternate_distributor_**'**  
 É o nome do Distribuidor do parceiro de sincronização alternativo. *alternate_distributor* está **sysname**, sem padrão.  
  
 [  **@friendly_name=**] **'**_Nome_amigável_**'**  
 É um nome para exibição pelo qual a associação de Publicador, publicação e Distribuidor que constituem um parceiro de sincronização alternativo pode ser identificada. *Nome_amigável* está **nvarchar (255)**, com um padrão NULL.  
  
 [  **@reserved=**] **'**_reservado_**'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addmergealternatepublisher** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_addmergealternatepublisher**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_dropmergealternatepublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergealternatepublisher-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
