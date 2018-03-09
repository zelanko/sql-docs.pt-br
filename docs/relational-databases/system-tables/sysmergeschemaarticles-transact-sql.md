---
title: sysmergeschemaarticles (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sysmergeschemaarticles_TSQL
- sysmergeschemaarticles
dev_langs: TSQL
helpviewer_keywords: sysmergeschemaarticles system table
ms.assetid: b5085979-2f76-48e1-bf3b-765a84003dd9
caps.latest.revision: "27"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 13a3104b8f457cf4c9d223630739e3cf6eb76ee8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergeschemaarticles-transact-sql"></a>sysmergeschemaarticles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Rastreia artigos somente esquema para replicação de mesclagem. Essa tabela é armazenada nos bancos de dados de publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|O nome do artigo somente esquema em uma publicação de mesclagem.|  
|**tipo**|**tinyint**|Indica o tipo de artigo somente esquema que pode ser um dos seguintes:<br /><br /> **0x20** = o artigo de somente esquema de procedimento armazenado.<br /><br /> **0x40** = artigo somente esquema de exibição ou artigo somente esquema de exibição indexada.|  
|**ObjID**|**int**|O identificador de objeto do objeto base do artigo. Pode ser o identificador de objeto de um procedimento, exibição indexada, exibição ou função definida pelo usuário.|  
|**artid**|**uniqueidentifier**|ID do artigo.|  
|**Descrição**|**nvarchar(255)**|A descrição do artigo.|  
|**pre_creation_command**|**tinyint**|A ação padrão a ser executada quando o artigo é criado no banco de dados de assinatura:<br /><br /> **0 =** nenhum - se a tabela já existir no assinante, nenhuma ação será tomada.<br /><br /> **1** = descartar - descarta a tabela antes de criá-lo novamente.<br /><br /> **2** = excluir-emite uma exclusão com base na cláusula WHERE no filtro de subconjunto.<br /><br /> **3** = truncar-igual **2**, mas exclui páginas em vez de linhas. Porém, não exige uma cláusula WHERE.|  
|**PubID**|**uniqueidentifier**|O identificador exclusivo da publicação.|  
|**status**|**tinyint**|Indica o status do artigo somente esquema, que pode ser um dos seguintes:<br /><br /> **1** = não sincronizado - o script de processamento inicial para publicar a tabela é executado na próxima vez em que o Snapshot Agent é executado.<br /><br /> **2** = ativo - o script de processamento inicial para publicar a tabela foi executado.<br /><br /> **5** = New_inactive - a ser adicionado.<br /><br /> **6** = New_active - a ser adicionado.|  
|**creation_script**|**nvarchar(255)**|O caminho e nome de um script de pré-criação de esquema de artigo opcional usado para criar a tabela de destino.|  
|**schema_option**|**binary (8)**|O bitmap da opção de geração de esquema para o artigo somente esquema determinado, que pode ser o resultado OR lógico bit a bit de um ou mais desses valores:<br /><br /> **0x00** = desabilitar geração de script pelo Snapshot Agent e usar o CreationScript fornecido.<br /><br /> **0x01** = gerar a criação do objeto (CREATE TABLE, CREATE PROCEDURE e assim por diante).<br /><br /> **0x10** = gerar um índice clusterizado correspondente.<br /><br /> **0x20** = converter tipos de dados definidos pelo usuário para tipos de dados base.<br /><br /> **0x40** = índice não clusterizado correspondente de gerar ou índices.<br /><br /> **0x80** = inclui integridade referencial declarada nas chaves primárias.<br /><br /> **0x100** = replicar gatilhos de usuário em um artigo de tabela, se definido.<br /><br /> **0x200** = replicar restrições de chave estrangeira. Se a tabela referenciada não for parte de uma publicação, todas as restrições de chave estrangeira em uma tabela publicada não serão replicadas.<br /><br /> **0x400** = replicar restrições de verificação.<br /><br /> **0x800** = replicar padrões.<br /><br /> **0x1000** = replicar agrupamento no nível de coluna.<br /><br /> **0x2000** = replicar propriedades estendidas associadas com o objeto de origem do artigo publicado.<br /><br /> **0x4000** = replicar chaves exclusivas definidas em um artigo de tabela.<br /><br /> **0x8000** = replicar uma chave primária e chaves exclusivas em uma tabela do artigo como restrições usando instruções ALTER TABLE.<br /><br /> Para obter mais informações sobre os valores possíveis para **schema_option**, consulte [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|O nome do objeto de destino no banco de dados de assinatura. Esse valor só se aplica a artigos somente esquema, como procedimentos armazenados, exibições e UDFs.|  
|**destination_owner**|**sysname**|O proprietário do objeto de banco de dados de assinatura, se não for **dbo**.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
