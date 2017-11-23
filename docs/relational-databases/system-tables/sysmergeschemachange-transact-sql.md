---
title: sysmergeschemachange (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sysmergeschemachange_TSQL
- sysmergeschemachange
dev_langs: TSQL
helpviewer_keywords: sysmergeschemachange system table
ms.assetid: ae9ce16e-6ee9-4c7c-8210-a9bf2c7efdf0
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f42fbeba8639216d5a95414430099fbd5bde0b07
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sysmergeschemachange-transact-sql"></a>sysmergeschemachange (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre os artigos publicados gerados pelo Snapshot Agent. Essa tabela é armazenada nos bancos de dados de publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**PubID**|**uniqueidentifier**|A ID da publicação.|  
|**artid**|**uniqueidentifier**|A ID do artigo.|  
|**schemaversion**|**int**|O número da última alteração de esquema.|  
|**schemaguid**|**uniqueidentifier**|A ID exclusiva do último esquema.|  
|**SchemaType**|**int**|O tipo de alteração do esquema:<br /><br /> **-1** = não é válido.<br /><br /> **1** = comando SQL.<br /><br /> **2** = script de esquema.<br /><br /> **3** = programa de cópia em massa nativo BCP (utilitário).<br /><br /> **4** = BCP de caractere.<br /><br /> **5** = última geração registrada.<br /><br /> **6** = última geração enviada.<br /><br /> **7** = diretório.<br /><br /> **8** = prioridade.<br /><br /> **9** = período de retenção.<br /><br /> **10** = script de gatilho.<br /><br /> **11** = Alter table.<br /><br /> **12** = reiniciar tudo.<br /><br /> **13** = ALTER TABLE (não -[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]).<br /><br /> **14** = reiniciar com carregamento.<br /><br /> **15** = script de restrição e índice.<br /><br /> **16** = limpeza de metadados.<br /><br /> **17** = atualizar última geração enviada.<br /><br /> **18** = nível de compatibilidade com versões anteriores.<br /><br /> **19** = validar informações de assinante.<br /><br /> **20** = bem particionado.<br /><br /> **21** = resolvedor personalizado.<br /><br /> **22** = ordem de processamento do artigo.<br /><br /> **23** = publicado em publicação transacional.<br /><br /> **24** = compensar erros.<br /><br /> **25** = pasta de instantâneo alternativo.<br /><br /> **26** = somente para download.<br /><br /> **27** = controle de exclusão.<br /><br /> **40** = script de instantâneo de pré-criação.<br /><br /> **45** = script de instantâneo de pós-criação.<br /><br /> **46** = script de usuário sob demanda.<br /><br /> **50** = cabeçalho de instantâneo começar.<br /><br /> **51** = término de cabeçalho de instantâneo.<br /><br /> **52** = trailer de instantâneo.<br /><br /> **53** = endereço de protocolo de transferência de arquivo (FTP).<br /><br /> **54** = porta de FTP.<br /><br /> **55** = subdiretório de FTP.<br /><br /> **56** = instantâneo compactado.<br /><br /> **57** = logon de FTP.<br /><br /> **58** = senha de FTP.<br /><br /> **60** = script de pré-criação de sistema.<br /><br /> **61** = esquema de procedimento armazenado.<br /><br /> **62** = esquema de exibição.<br /><br /> **63** = esquema de função definida pelo usuário.<br /><br /> **64** = índices de exibição.<br /><br /> **65** = propriedades estendidas.<br /><br /> **66** = validar.<br /><br /> **67** = comando SQL de pré-instantâneo.<br /><br /> **71** = validação de instantâneo dinâmico.<br /><br /> **80** = sistema BCP 9.0 nativo de tabela.<br /><br /> **81** = BCP 9.0 de caractere de tabela do sistema.<br /><br /> **82** = sistema nativo BCP 9.0 (somente global) de tabela.<br /><br /> **83** = BCP 9.0 (somente global) de caractere de tabela do sistema.<br /><br /> **84** = sistema BCP 9.0 (lightweight) nativo de tabela.<br /><br /> **85** = BCP 9.0 (lightweight) de caractere de tabela do sistema.<br /><br /> **128** = BCP dinâmico (bits).<br /><br /> **131** = BCP nativo dinâmico.<br /><br /> **132** = BCP de caractere dinâmico.<br /><br /> **208** = dinâmico BCP 9.0 nativo de tabela do sistema.<br /><br /> **209** = BCP 9.0 de caractere de tabela de sistema dinâmico.<br /><br /> **210** = dinâmico nativo BCP 9.0 (somente global) da tabela de sistema.<br /><br /> **211** = BCP 9.0 (somente global) de caractere de tabela de sistema dinâmico.<br /><br /> **212** = dinâmico BCP 9.0 (lightweight) nativo de tabela do sistema.<br /><br /> **213** = BCP 9.0 (lightweight) de caractere de tabela de sistema dinâmico.<br /><br /> **300** = ações data Definition Language (DDL).<br /><br /> **1024** = controle de instantâneo incremental.<br /><br /> **1049** = pasta de instantâneo incremental.<br /><br /> **1074** = Incremental cabeçalho de início do instantâneo.<br /><br /> **1075** = cabeçalho de término de instantâneo incremental.<br /><br /> **1076** = trailer de instantâneo incremental.<br /><br /> **1077** = endereço de FTP incremental.<br /><br /> **1078** = porta de FTP incremental.<br /><br /> **1079** = subdiretório de FTP incremental.<br /><br /> **1080** = instantâneo compactado incremental.<br /><br /> **1081** = logon de FTP incremental.<br /><br /> **1082** = senha de FTP incremental.|  
|**schematext**|**nvarchar(2000)**|O nome do arquivo de script ou um comando que inclui um nome de arquivo|  
|**schemastatus**|**tinyint**|Indica se uma alteração de esquema está pendente para o artigo que pode ser um dos valores seguintes:<br /><br /> **0** = inativo.<br /><br /> **1** = ativo.<br /><br /> Quando uma alteração de esquema está pendente, esse valor é definido como **1**.|  
|**schemasubtype**|**int**|O subtipo de alteração do esquema:<br /><br /> **1** = ADDCOLUMN<br /><br /> **2** = DROPCOLUMN<br /><br /> **3** = ALTERCOLUMN<br /><br /> **4** = ADDPRIMARYKEY<br /><br /> **5** = ADDUNIQUE<br /><br /> **6** = ADICIONAR REFERÊNCIA<br /><br /> **7** = DROPCONSTRAINT<br /><br /> **8** = ADDDEFAULT<br /><br /> **9** = ADDCHECK<br /><br /> **10** = DISABLETRIGGER<br /><br /> **11** = ENABLETRIGGER<br /><br /> **12** = DISABLETRIGGER<br /><br /> **13** = ENABLETRIGGER<br /><br /> **14** = ENABLECONSTRAINT<br /><br /> **15** = DISABLECONSTRAINT<br /><br /> **16** = ENABLECONSTRAINT<br /><br /> **17** = DISABLECONSTRAINT|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
