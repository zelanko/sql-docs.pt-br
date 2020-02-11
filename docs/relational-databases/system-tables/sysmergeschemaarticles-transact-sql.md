---
title: sysmergeschemaarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeschemaarticles_TSQL
- sysmergeschemaarticles
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemaarticles system table
ms.assetid: b5085979-2f76-48e1-bf3b-765a84003dd9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9446d03db98d7fa5181fb0217814cdd86c55de1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029814"
---
# <a name="sysmergeschemaarticles-transact-sql"></a>sysmergeschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rastreia artigos somente esquema para replicação de mesclagem. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome do artigo somente esquema em uma publicação de mesclagem.|  
|**tipo**|**tinyint**|Indica o tipo de artigo somente esquema que pode ser um dos seguintes:<br /><br /> **0x20** = artigo de somente esquema de procedimento armazenado.<br /><br /> **0x40** = exibir somente esquema ou artigo somente esquema de exibição indexada.|  
|**objID**|**int**|O identificador de objeto do objeto base do artigo. Pode ser o identificador de objeto de um procedimento, exibição indexada, exibição ou função definida pelo usuário.|  
|**artid**|**uniqueidentifier**|A ID do artigo.|  
|**ndescrição**|**nvarchar (255)**|A descrição do artigo.|  
|**pre_creation_command**|**tinyint**|A ação padrão a ser executada quando o artigo é criado no banco de dados de assinatura:<br /><br /> **0 =** Nenhum – se a tabela já existir no Assinante, nenhuma ação será executada.<br /><br /> **1** = drop-remove a tabela antes de recriá-la.<br /><br /> **2** = Delete-emite uma exclusão com base na cláusula WHERE no filtro de subconjunto.<br /><br /> **3** = truncar-igual a **2**, mas exclui páginas em vez de linhas. Porém, não exige uma cláusula WHERE.|  
|**pubid**|**uniqueidentifier**|O identificador exclusivo da publicação.|  
|**status**|**tinyint**|Indica o status do artigo somente esquema, que pode ser um dos seguintes:<br /><br /> **1** = não sincronizado – o script de processamento inicial para publicar a tabela é executado na próxima vez que o agente de instantâneo for executado.<br /><br /> **2** = ativo-o script de processamento inicial para publicar a tabela foi executado.<br /><br /> **5** = New_inactive-a ser adicionado.<br /><br /> **6** = New_active-a ser adicionado.|  
|**creation_script**|**nvarchar (255)**|O caminho e nome de um script de pré-criação de esquema de artigo opcional usado para criar a tabela de destino.|  
|**schema_option**|**binário (8)**|O bitmap da opção de geração de esquema para o artigo somente esquema determinado, que pode ser o resultado OR lógico bit a bit de um ou mais desses valores:<br /><br /> **0x00** = desabilitar o script pelo agente de instantâneo e usa o CreationScript fornecido.<br /><br /> **0x01** = gerar a criação do objeto (CREATE TABLE, criar procedimento e assim por diante).<br /><br /> **0x10** = gerar um índice clusterizado correspondente.<br /><br /> **0x20** = converter tipos de dados definidos pelo usuário em tipos de dados base.<br /><br /> **0x40** = gerar índice ou índices não clusterizados correspondentes.<br /><br /> **0x80** = incluir integridade referencial declarada nas chaves primárias.<br /><br /> **0x100** = replicar gatilhos de usuário em um artigo de tabela, se definido.<br /><br /> **0x200** = replicar restrições Foreign Key. Se a tabela referenciada não for parte de uma publicação, todas as restrições de chave estrangeira em uma tabela publicada não serão replicadas.<br /><br /> **0x400** = replicar restrições de verificação.<br /><br /> **0x800** = replicar padrões.<br /><br /> **0x1000** = replicar agrupamento em nível de coluna.<br /><br /> **0x2000** = replicar propriedades estendidas associadas ao objeto de origem do artigo publicado.<br /><br /> **0x4000** = replicar chaves exclusivas, se definido em um artigo de tabela.<br /><br /> **0x8000** = replicar uma chave primária e chaves exclusivas em um artigo de tabela como restrições usando instruções ALTER TABLE.<br /><br /> Para obter mais informações sobre os valores possíveis para **schema_option**, consulte [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|O nome do objeto de destino no banco de dados de assinatura. Esse valor só se aplica a artigos somente esquema, como procedimentos armazenados, exibições e UDFs.|  
|**destination_owner**|**sysname**|O proprietário do objeto no banco de dados de assinatura, se não for **dbo**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
