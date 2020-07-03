---
title: sysmergeschemachange (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergeschemachange_TSQL
- sysmergeschemachange
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeschemachange system table
ms.assetid: ae9ce16e-6ee9-4c7c-8210-a9bf2c7efdf0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7740982430f03aed138a578dc12113eb7caf1764
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881351"
---
# <a name="sysmergeschemachange-transact-sql"></a>sysmergeschemachange (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém informações sobre os artigos publicados gerados pelo Snapshot Agent. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**pubid**|**uniqueidentifier**|A ID da publicação.|  
|**artid**|**uniqueidentifier**|A ID do artigo.|  
|**SchemaVersion**|**int**|O número da última alteração de esquema.|  
|**schemaguid**|**uniqueidentifier**|A ID exclusiva do último esquema.|  
|**schematype**|**int**|O tipo de alteração do esquema:<br /><br /> **-1** = inválido.<br /><br /> **1** = comando SQL.<br /><br /> **2** = script de esquema.<br /><br /> **3** = bcp (utilitário de programa de cópia em massa) nativo.<br /><br /> **4** = caractere bcp.<br /><br /> **5** = última geração gravada.<br /><br /> **6** = última geração enviada.<br /><br /> **7** = diretório.<br /><br /> **8** = prioridade.<br /><br /> **9** = período de retenção.<br /><br /> **10** = script de gatilho.<br /><br /> **11** = ALTER TABLE.<br /><br /> **12** = reinicializar tudo.<br /><br /> **13** = ALTER TABLE (não- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ).<br /><br /> **14** = reinicializar com upload.<br /><br /> **15** = script de restrição e de índice.<br /><br /> **16** = limpeza de metadados.<br /><br /> **17** = atualização da última geração enviada.<br /><br /> **18** = nível de compatibilidade com versões anteriores.<br /><br /> **19** = validar informações do Assinante.<br /><br /> **20** = bem particionado.<br /><br /> **21** = resolvedor personalizado.<br /><br /> **22** = ordem de processamento do artigo.<br /><br /> **23** = publicado na publicação transacional.<br /><br /> **24** = compensar erros.<br /><br /> **25** = pasta de instantâneo alternativa.<br /><br /> **26** = somente para download.<br /><br /> **27** = excluir controle.<br /><br /> **40** = script de instantâneo de pré-criação.<br /><br /> **45** = script de instantâneo após a criação.<br /><br /> **46** = script de usuário sob demanda.<br /><br /> **50** = início do cabeçalho do instantâneo.<br /><br /> **51** = fim do cabeçalho do instantâneo.<br /><br /> **52** = trailer de instantâneo.<br /><br /> **53** = endereço protocolo FTP (FTP).<br /><br /> **54** = porta de FTP.<br /><br /> **55** = subdiretório FTP.<br /><br /> **56** = instantâneo compactado.<br /><br /> **57** = logon de FTP.<br /><br /> **58** = senha de FTP.<br /><br /> **60** = script de pré-criação do sistema.<br /><br /> **61** = esquema de procedimento armazenado.<br /><br /> **62** = exibir esquema.<br /><br /> **63** = esquema de função definido pelo usuário.<br /><br /> **64** = exibir índices.<br /><br /> **65** = propriedades estendidas.<br /><br /> **66** = validar.<br /><br /> **67** = comando SQL de pré-instantâneo.<br /><br /> **71** = validação dinâmica de instantâneo.<br /><br /> **80** = tabela do sistema BCP Native 9,0.<br /><br /> **81** = caractere de tabela do sistema BCP 9,0.<br /><br /> **82** = tabela do sistema BCP Native 9,0 (somente global).<br /><br /> **83** = caractere de tabela do sistema BCP 9,0 (somente global).<br /><br /> **84** = tabela do sistema BCP Native 9,0 (leve).<br /><br /> **85** = caractere de tabela do sistema BCP 9,0 (leve).<br /><br /> **128** = bcp dinâmico (bit).<br /><br /> **131** = bcp nativo dinâmico.<br /><br /> **132** = caractere dinâmico bcp.<br /><br /> **208** = native BCP 9,0 da tabela de sistema dinâmica.<br /><br /> **209** = caractere de tabela de sistema dinâmico BCP 9,0.<br /><br /> **210** = tabela dinâmica de sistema dinâmico BCP 9,0 (somente global).<br /><br /> **211** = caractere de tabela de sistema dinâmico BCP 9,0 (somente global).<br /><br /> **212** = native BCP 9,0 (Lightweight) da tabela de sistema dinâmica.<br /><br /> **213** = caractere de tabela do sistema dinâmico BCP 9,0 (Lightweight).<br /><br /> **300** = ações DDL (linguagem de definição de dados).<br /><br /> **1024** = controle de instantâneo incremental.<br /><br /> **1049** = pasta de instantâneo incremental.<br /><br /> **1074** = cabeçalho de início do instantâneo incremental.<br /><br /> **1075** = cabeçalho de término do instantâneo incremental.<br /><br /> **1076** = trailer de instantâneo incremental.<br /><br /> **1077** = endereço FTP incremental.<br /><br /> **1078** = porta ftp incremental.<br /><br /> **1079** = subdiretório FTP incremental.<br /><br /> **1080** = instantâneo compactado incremental.<br /><br /> **1081** = logon de FTP incremental.<br /><br /> **1082** = senha de FTP incremental.|  
|**schematext**|**nvarchar (2000)**|O nome do arquivo de script ou um comando que inclui um nome de arquivo|  
|**schemastatus**|**tinyint**|Indica se uma alteração de esquema está pendente para o artigo que pode ser um dos valores seguintes:<br /><br /> **0** = inativo.<br /><br /> **1** = ativo.<br /><br /> Quando uma alteração de esquema estiver pendente, esse valor será definido como **1**.|  
|**schemasubtype**|**int**|O subtipo de alteração do esquema:<br /><br /> **1** = AddColumn<br /><br /> **2** = DROPCOLUMN<br /><br /> **3** = ALTERCOLUMN<br /><br /> **4** = addprimarykey<br /><br /> **5** = AddUnique<br /><br /> **6** = AddReference<br /><br /> **7** = DROPCONSTRAINT<br /><br /> **8** = ADDDEFAULT<br /><br /> **9** = addcheck<br /><br /> **10** = DISABLETRIGGER<br /><br /> **11** = ENABLETRIGGER<br /><br /> **12** = DISABLETRIGGER<br /><br /> **13** = ENABLETRIGGER<br /><br /> **14** = ENABLECONSTRAINT<br /><br /> **15** = DISABLECONSTRAINT<br /><br /> **16** = ENABLECONSTRAINT<br /><br /> **17** = DISABLECONSTRAINT|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
