---
title: MSpublications (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSpublications
- MSpublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublications system table
ms.assetid: 7a0b3457-7265-4f24-a255-7f055d908f20
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6e104407394925f5deb8d7d11a55fe8e979934df
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mspublications-transact-sql"></a>MSpublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSpublications** tabela contém uma linha para cada publicação replicada por um fornecedor. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|A ID do publicador.|  
|**publisher_db**|**sysname**|O nome do banco de dados Publicador.|  
|**Publicação**|**sysname**|O nome da publicação.|  
|**publication_id**|**Int**|A ID da publicação.|  
|**publication_type**|**Int**|O tipo de publicação:<br /><br /> **0** = transacional.<br /><br /> **1** = instantâneo.<br /><br /> **2** = mesclagem.|  
|**thirdparty_flag**|**bit**|Indica se uma publicação é um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados:<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> **1** = fonte de dados diferente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**independent_agent**|**bit**|Indica se existe um Distribution Agent autônomo para essa publicação.|  
|**immediate_sync**|**bit**|Indica se arquivos de sincronização são criados ou recriados cada vez que o Snapshot Agent é executado.|  
|**allow_push**|**bit**|Indica se podem ser criadas assinaturas push para a publicação determinada.|  
|**allow_pull**|**bit**|Indica se podem ser criadas assinaturas pull para a publicação determinada.|  
|**allow_anonymous**|**bit**|Indica se podem ser criadas assinaturas anônimas para a publicação determinada.|  
|**Descrição**|**nvarchar(255)**|A descrição da publicação.|  
|**VENDOR_NAME**|**nvarchar(100)**|O nome do fornecedor se Publicador não for um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**retention**|**Int**|O período de retenção da publicação, em horas.|  
|**sync_method**|**Int**|O método de sincronização:<br /><br /> **0** = nativo (produz saída de cópia em massa em modo nativo de todas as tabelas).<br /><br /> **1** = caractere (produz uma saída de cópia em massa em modo de caractere de todas as tabelas).<br /><br /> **3** = simultâneo (produz saída de cópia em massa em modo nativo de todas as tabelas, mas não bloqueia a tabela durante o instantâneo).<br /><br /> **4** = simultâneo (produz uma saída de cópia em massa em modo de caractere de todas as tabelas, mas não bloqueia a tabela durante o instantâneo)<br /><br /> Os valores **3** e **4** estão disponíveis para replicação transacional e replicação de mesclagem, mas não para replicação de instantâneo.|  
|**allow_subscription_copy**|**bit**|Habilita ou desabilita a capacidade para copiar os bancos de dados de assinatura que assinam essa publicação. **0** significa que a cópia está desabilitada e **1** significa que ele está habilitado.|  
|**thirdparty_options**|**Int**|Especifica se a exibição de uma publicação na pasta replicação do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é suprimida:<br /><br /> **0** = exibir uma publicação heterogênea na pasta replicação do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].<br /><br /> **1** = suprimir a exibição uma publicação heterogênea na pasta replicação do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|**allow_queued_tran**|**bit**|Especifica se a publicação permite atualização enfileirada:<br /><br /> **0 =** publicação não é enfileirada.<br /><br /> **1** = publicação é enfileirada.|  
|**Opções**|**Int**|Nenhuma informação está disponível para esta versão.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
