---
title: OBJECTPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OBJECTPROPERTY
- OBJECTPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying schema-scoped object information
- viewing schema-scoped object information
- OBJECTPROPERTY function
- schema-scoped objects [SQL Server]
- objects [SQL Server], schema-scoped
ms.assetid: 27569888-f8b5-4cec-a79f-6ea6d692b4ae
caps.latest.revision: 81
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 2189ba0ca7245fcd098d2af55b381afc465a7fab
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="objectproperty-transact-sql"></a>OBJECTPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações sobre objetos no escopo do esquema no banco de dados atual. Para obter uma lista de objetos no escopo do esquema, consulte [sys. Objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). Essa função não pode ser usada por objetos que não sejam de escopo de esquema, como gatilhos DDL (linguagem de definição de dados) e notificações de eventos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
OBJECTPROPERTY ( id , property )   
```  
  
## <a name="arguments"></a>Argumentos  
 *id*  
 É uma expressão que representa a ID do objeto no banco de dados atual. *ID* é **int** e é considerado como um objeto no escopo do esquema no contexto do banco de dados atual.  
  
 *propriedade*  
 É uma expressão que representa as informações a serem retornadas para o objeto especificado pelo *id*. *propriedade* pode ser um dos valores a seguir.  
  
> [!NOTE]  
>  A menos que indicado em contrário, NULL é retornado quando *propriedade* não é um nome de propriedade válido, *id* não é uma ID de objeto válido, *id* é um tipo de objeto sem suporte especificado *propriedade*, ou o chamador não tem permissão para exibir os metadados do objeto.  
  
|Nome da propriedade|Tipo de objeto|Descrição e valores retornados|  
|-------------------|-----------------|-------------------------------------|  
|CnstIsClustKey|Constraint|Restrição PRIMARY KEY com um índice clusterizado.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsColumn|Constraint|Restrição CHECK, DEFAULT ou FOREIGN KEY em uma única coluna.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsDeleteCascade|Constraint|Restrição FOREIGN KEY com a opção ON DELETE CASCADE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsDisabled|Constraint|Restrição desabilitada.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNonclustKey|Constraint|Restrição PRIMARY KEY ou UNIQUE com um índice não clusterizado.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNotRepl|Constraint|A restrição é definida por meio das palavras-chave NOT FOR REPLICATION.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsNotTrusted|Constraint|A restrição estava habilitada sem verificação das linhas existentes; portanto, a restrição pode não se manter para todas as linhas.<br /><br /> 1 = True<br /><br /> 0 = False|  
|CnstIsUpdateCascade|Constraint|Restrição FOREIGN KEY com a opção ON UPDATE CASCADE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsAfterTrigger|Gatilho|Gatilho AFTER.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsAnsiNullsOn|Função [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)], gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)], exibição|Configuração de ANSI_NULLS no momento da criação.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsDeleteTrigger|Gatilho|Gatilho DELETE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstDeleteTrigger|Gatilho|Primeiro gatilho acionado quando DELETE é executada na tabela.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstInsertTrigger|Gatilho|Primeiro gatilho acionado quando INSERT é executada na tabela.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsFirstUpdateTrigger|Gatilho|Primeiro gatilho acionado quando UPDATE é executada na tabela.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsInsertTrigger|Gatilho|Gatilho INSERT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsInsteadOfTrigger|Gatilho|Gatilho INSTEAD OF.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastDeleteTrigger|Gatilho|Último gatilho acionado quando DELETE é executado na tabela.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastInsertTrigger|Gatilho|Último gatilho acionado quando INSERT é executado na tabela.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsLastUpdateTrigger|Gatilho|Último gatilho acionado quando UPDATE é executado na tabela.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsQuotedIdentOn|Função [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)], gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)], exibição|Configuração de QUOTED_IDENTIFIER na criação.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsStartup|Procedimento|Procedimento de inicialização.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsTriggerDisabled|Gatilho|Gatilho desabilitado.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsTriggerNotForRepl|Gatilho|Gatilho definido como NOT FOR REPLICATION.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsUpdateTrigger|Gatilho|Gatilho UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|ExecIsWithNativeCompilation|Procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)]|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> O procedimento é compilado nativamente.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|HasAfterTrigger|Tabela, exibição|A tabela ou exibição tem um gatilho AFTER.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasDeleteTrigger|Tabela, exibição|A tabela ou exibição tem um gatilho DELETE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasInsertTrigger|Tabela, exibição|A tabela ou exibição tem um gatilho INSERT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasInsteadOfTrigger|Tabela, exibição|A tabela ou exibição tem um gatilho INSTEAD OF.<br /><br /> 1 = True<br /><br /> 0 = False|  
|HasUpdateTrigger|Tabela, exibição|A tabela ou exibição tem um gatilho UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsAnsiNullsOn|Função [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)], tabela, gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)], exibição|Especifica que a configuração da opção ANSI NULLS para a tabela está ON. Isso significa que todas as comparações com um valor nulo são avaliadas como UNKNOWN. Essa configuração se aplica a todas as expressões na definição da tabela, inclusive colunas computadas e restrições, enquanto a tabela existir.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsCheckCnst|Qualquer objeto no escopo do esquema|Restrição CHECK.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsConstraint|Qualquer objeto no escopo do esquema|É uma restrição de coluna única CHECK, DEFAULT ou FOREIGN KEY em uma coluna ou tabela.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDefault|Qualquer objeto no escopo do esquema|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Padrão associado.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDefaultCnst|Qualquer objeto no escopo do esquema|Restrição DEFAULT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsDeterministic|Função, exibição|A propriedade determinista da função ou exibição.<br /><br /> 1 = Determinista<br /><br /> 0 = Não determinista|  
|IsEncrypted|Função [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)], tabela, gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)], exibição|Indica que o texto original da instrução de módulo foi convertido para um formato ofuscado. A saída do ofuscamento não é diretamente visível em quaisquer exibições de catálogo no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Os usuários que não tiverem acesso a tabelas do sistema ou arquivos do banco de dados não poderão recuperar o texto ofuscado. No entanto, o texto está disponível para os usuários que puderem acessar as tabelas do sistema sobre a [porta DAC](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) ou acessar diretamente os arquivos de banco de dados. Além disso, os usuários que podem anexar um depurador ao processo de servidor também podem recuperar o procedimento original da memória em tempo de execução.<br /><br /> 1 = Criptografado<br /><br /> 0 = não criptografado<br /><br /> Tipo de dados base: **int**|  
|IsExecuted|Qualquer objeto no escopo do esquema|O objeto pode ser executado (exibição, procedimento, função ou gatilho).<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsExtendedProc|Qualquer objeto no escopo do esquema|Procedimento estendido.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsForeignKey|Qualquer objeto no escopo do esquema|Restrição FOREIGN KEY.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsIndexed|Tabela, exibição|A tabela ou exibição que tem um índice.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsIndexable|Tabela, exibição|Tabela ou exibição na qual um índice pode ser criado.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsInlineFunction|Função|Função embutida.<br /><br /> 1 = Função embutida<br /><br /> 0 = Função não embutida|  
|IsMSShipped|Qualquer objeto no escopo do esquema|Objeto criado durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsPrimaryKey|Qualquer objeto no escopo do esquema|Restrição PRIMARY KEY.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> NULL = Não é uma função, ou a ID do objeto não é válida.|  
|IsProcedure|Qualquer objeto no escopo do esquema|Procedimento.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsQuotedIdentOn|Função [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)], tabela, gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)], exibição, restrição CHECK, definição DEFAULT|Especifica que a configuração de identificador citada para o objeto é ON. Isso significa que aspas duplas delimitam identificadores em todas as expressões envolvidas na definição do objeto.<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|IsQueue|Qualquer objeto no escopo do esquema|Fila do Service Broker<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsReplProc|Qualquer objeto no escopo do esquema|Procedimento de replicação.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsRule|Qualquer objeto no escopo do esquema|Regra associada.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsScalarFunction|Função|Função de valor escalar.<br /><br /> 1 = Função de valor escalar<br /><br /> 0 = Função com valor não escalar|  
|IsSchemaBound|Função, exibição|Uma função associada a esquema ou exibição criada usando SCHEMABINDING.<br /><br /> 1 = Associada a esquema<br /><br /> 0 = Não associada a esquema.|  
|IsSystemTable|Table|Tabela do sistema.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsTable|Table|Tabela.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsTableFunction|Função|Função com valor de tabela.<br /><br /> 1 = Função com valor de tabela<br /><br /> 0 = Função sem valor de tabela|  
|IsTrigger|Qualquer objeto no escopo do esquema|Gatilho.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsUniqueCnst|Qualquer objeto no escopo do esquema|Restrição UNIQUE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsUserTable|Table|Tabela definida pelo usuário.<br /><br /> 1 = True<br /><br /> 0 = False|  
|IsView|Exibição|Exibição.<br /><br /> 1 = True<br /><br /> 0 = False|  
|OwnerId|Qualquer objeto no escopo do esquema|Proprietário do objeto.<br /><br /> **Observação:** proprietário do esquema não é necessariamente o proprietário do objeto. Por exemplo, os objetos filho (aqueles em que *parent_object_id* for não nulo) sempre retornará a mesma ID de proprietário que o pai.<br /><br /> Não nula = A ID de usuário do banco de dados do proprietário do objeto.|  
|TableDeleteTrigger|Table|A tabela tem um gatilho DELETE.<br /><br /> > 1 = ID do primeiro gatilho com o tipo especificado.|  
|TableDeleteTriggerCount|Table|A tabela tem o número especificado de gatilhos DELETE.<br /><br /> >0 = O número de gatilhos DELETE.|  
|TableFullTextMergeStatus|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Se uma tabela que tem um índice de texto completo está atualmente em mesclagem.<br /><br /> 0 = A tabela não tem um índice de texto completo ou o índice de texto completo não está sendo mesclado.<br /><br /> 1 = O índice de texto completo está em mesclagem.|  
|TableFullTextBackgroundUpdateIndexOn|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> A tabela tem índice de atualização em segundo plano de texto completo (controle de alteração automática) habilitado.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE|  
|TableFulltextCatalogId|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID do catálogo de texto completo no qual residem os dados do índice de texto completo para a tabela.<br /><br /> Diferente de zero = ID de catálogo de texto completo associado ao índice exclusivo que identifica as linhas em uma tabela indexada de texto completo.<br /><br /> 0 = A tabela não tem um índice de texto completo.|  
|TableFulltextChangeTrackingOn|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> O controle de alterações de texto completo da tabela está habilitado.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE|  
|TableFulltextDocsProcessed|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de linhas processadas desde o início da indexação de texto completo. Em uma tabela que está sendo indexada para pesquisa de texto completo, todas as colunas de uma linha são consideradas parte de um documento a ser indexado.<br /><br /> 0 = Nenhum rastreamento ativo ou indexação de texto completo está concluído.<br /><br /> > 0 = uma das opções a seguir (A ou B): A) o número de documentos processados pelas inserir ou atualizar operações desde o início do completo, Incremental ou Manual de população de controle de alterações. B) o número de linhas processadas pelo insert ou operações de atualização desde a habilitação do controle de alterações com população de índice de atualização em segundo plano, o esquema de índice de texto completo alterado, o catálogo de texto completo recriado ou a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reiniciado e assim por diante.<br /><br /> NULL = A tabela não tem um índice de texto completo.<br /><br /> Essa propriedade não monitora nem conta linhas excluídas.|  
|TableFulltextFailCount|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de linhas que a Pesquisa de Texto Completo não indexou.<br /><br /> 0 = A população foi concluída.<br /><br /> > 0 = uma das opções a seguir (A ou B): A) o número de documentos que não foram indexados desde o início da população de controle de alterações completo, Incremental ou Manual. B) índice, o número de linhas que não foram indexados desde o início da população ou o reinício da população de atualização para o controle de alterações com o plano de fundo. Isso pode ter sido causado por uma alteração de esquema, recriação do catálogo, reinicialização de servidor, etc.<br /><br /> NULL = A tabela não tem um índice de texto completo.|  
|TableFulltextItemCount|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de linhas que foram indexadas com texto completo com êxito.|  
|TableFulltextKeyColumn|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID da coluna associada ao índice exclusivo de coluna única que participa da definição do índice de texto completo.<br /><br /> 0 = A tabela não tem um índice de texto completo.|  
|TableFulltextPendingChanges|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de entradas de controle de alterações pendentes a serem processadas.<br /><br /> 0 = o controle de alterações não está habilitado.<br /><br /> NULL = A tabela não tem um índice de texto completo.|  
|TableFulltextPopulateStatus|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = Ocioso<br /><br /> 1 = População completa em andamento.<br /><br /> 2 = População incremental em andamento.<br /><br /> 3 = Propagação de alterações controladas em andamento.<br /><br /> 4 = Índice de atualização em segundo plano em andamento, bem como controle de alteração automática.<br /><br /> 5 = Indexação de texto completo acelerado ou pausado.|  
|TableHasActiveFulltextIndex|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> A tabela tem um índice de texto completo ativo.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasCheckCnst|Table|A tabela tem uma restrição CHECK.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasClustIndex|Table|A tabela tem um índice clusterizado.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasDefaultCnst|Table|A tabela tem uma restrição DEFAULT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasDeleteTrigger|Table|A tabela tem um gatilho DELETE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasForeignKey|Table|A tabela tem uma restrição FOREIGN KEY.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasForeignRef|Table|A tabela é referenciada por uma restrição FOREIGN KEY.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasIdentity|Table|A tabela tem uma coluna de identidade.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasIndex|Table|A tabela tem um índice de qualquer tipo.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasInsertTrigger|Table|O objeto tem um gatilho INSERT.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasNonclustIndex|Table|A tabela tem um índice não clusterizado.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasPrimaryKey|Table|A tabela tem uma chave primária.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasRowGuidCol|Table|Tabela possui um ROWGUIDCOL para uma **uniqueidentifier** coluna.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasTextImage|Table|A tabela tem um **texto**, **ntext**, ou **imagem** coluna.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasTimestamp|Table|A tabela tem um **timestamp** coluna.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasUniqueCnst|Table|A tabela tem uma restrição UNIQUE.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasUpdateTrigger|Table|Objeto tem um gatilho de atualização.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableHasVarDecimalStorageFormat|Table|Tabela está habilitada para **vardecimal** o formato de armazenamento.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableInsertTrigger|Table|A tabela tem um gatilho INSERT.<br /><br /> > 1 = ID do primeiro gatilho com o tipo especificado.|  
|TableInsertTriggerCount|Table|Tabela tem o número especificado de gatilhos de inserção.<br /><br /> >0 = O número de gatilhos INSERT.|  
|TableIsFake|Table|A tabela não é real. Ela é materializada internamente sob demanda pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableIsLockedOnBulkLoad|Table|Tabela é bloqueada devido a um **bcp** ou trabalho de inserção em MASSA.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableIsMemoryOptimized|Table|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> A tabela tem otimização de memória<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**<br /><br /> Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).|  
|TableIsPinned|Table|A tabela está fixada para ser mantida no cache de dados.<br /><br /> 0 = False<br /><br /> Esse recurso não tem suporte no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e em versões posteriores.|  
|TableTextInRowLimit|Table|Máximo de bytes permitidos para text in row.<br /><br /> 0 se a opção text in row não estiver definida.|  
|TableUpdateTrigger|Table|A tabela tem um gatilho UPDATE.<br /><br /> > 1 = ID do primeiro gatilho com o tipo especificado.|  
|TableUpdateTriggerCount|Table|A tabela tem o número especificado de gatilhos UPDATE.<br /><br /> > 0 = O número de gatilhos UPDATE.|  
|TableHasColumnSet|Table|A tabela tem um conjunto de colunas.<br /><br /> 0 = False<br /><br /> 1 = True<br /><br /> Para obter mais informações, veja [Usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md).|  
|TableTemporalType|Table|**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica o tipo de tabela.<br /><br /> 0 = a tabela não temporal<br /><br /> 1 = a tabela de histórico para tabela com versão do sistema<br /><br /> 2 = a tabela temporal com versão do sistema|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que as funções internas emissoras de metadados, como OBJECTPROPERTY, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] supõe que *object_id* está no contexto do banco de dados atual. Uma consulta que faz referência a um *object_id* em outro banco de dados retornará NULL ou resultados incorretos. Por exemplo, na consulta a seguir, o contexto do banco de dados atual é o banco de dados mestre. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentará retornar o valor da propriedade especificado *object_id* no banco de dados em vez de banco de dados especificado na consulta. A consulta retorna resultados incorretos, pois o modo de exibição `vEmployee` não está no banco de dados mestre.  
  
```  
USE master;  
GO  
SELECT OBJECTPROPERTY(OBJECT_ID(N'AdventureWorks2012.HumanResources.vEmployee'), 'IsView');  
GO  
```  
  
 OBJECTPROPERTY (*view_id*, 'IsIndexable') pode consumir recursos significativos do computador porque a avaliação da propriedade IsIndexable requer a análise da definição da exibição, normalização e otimização parcial. Embora a propriedade IsIndexable identifique tabelas ou exibições que podem ser indexadas, a criação atual do índice ainda poderá falhar se certos requisitos de chave de índice não forem atendidos. Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 OBJECTPROPERTY (*table_id*, 'TableHasActiveFulltextIndex') retornará um valor de 1 (verdadeiro) quando pelo menos uma coluna de uma tabela for adicionada para indexação. A indexação de texto completo será ativada automaticamente para população assim que a primeira coluna for adicionada para indexação.  
  
 Quando uma tabela é criada, a opção QUOTED IDENTIFIER sempre é armazenada como ON nos metadados da tabela, mesmo que a opção esteja definida como OFF quando a tabela é criada. Portanto, OBJECTPROPERTY (*table_id*, 'IsQuotedIdentOn') sempre retornará um valor de 1 (verdadeiro).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-verifying-that-an-object-is-a-table"></a>A. Verificando se um objeto é uma tabela  
 O exemplo a seguir testa se `UnitMeasure` é uma tabela no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') = 1  
   PRINT 'UnitMeasure is a table.'  
ELSE IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') = 0  
   PRINT 'UnitMeasure is not a table.'  
ELSE IF OBJECTPROPERTY (OBJECT_ID(N'Production.UnitMeasure'),'ISTABLE') IS NULL  
   PRINT 'ERROR: UnitMeasure is not a valid object.';  
GO  
  
```  
  
### <a name="b-verifying-that-a-scalar-valued-user-defined-function-is-deterministic"></a>B. Verificando se uma função definida pelo usuário de valor escalar é determinística  
 A exemplo a seguir testa se a função de valor escalar definida pelo usuário `ufnGetProductDealerPrice`, que retorna um **money** valor, é determinística.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECTPROPERTY(OBJECT_ID('dbo.ufnGetProductDealerPrice'), 'IsDeterministic');  
GO  
```  
  
 O conjunto de resultados mostra que `ufnGetProductDealerPrice` não é uma função determinística.  
  
 ```
-----  
0
```  
  
### <a name="c-finding-the-tables-that-belong-to-a-specific-schema"></a>C: Localizando tabelas que pertencem a um esquema específico  
 O exemplo a seguir retorna todas as tabelas no esquema dbo.  
  
```  
-- Uses AdventureWorks  
  
SELECT name, object_id, type_desc  
FROM sys.objects   
WHERE OBJECTPROPERTY(object_id, N'SchemaId') = SCHEMA_ID(N'dbo')  
ORDER BY type_desc, name;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-verifying-that-an-object-is-a-table"></a>Verificando se um objeto é uma tabela de unidade d:  
 O exemplo a seguir testa se `dbo.DimReseller` é uma tabela no banco de dados [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].  
  
```  
-- Uses AdventureWorks  
  
IF OBJECTPROPERTY (OBJECT_ID(N'dbo.DimReseller'),'ISTABLE') = 1  
   SELECT 'DimReseller is a table.'  
ELSE   
   SELECT 'DimReseller is not a table.';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [COLUMNPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTYEX &#40; Transact-SQL &#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  


