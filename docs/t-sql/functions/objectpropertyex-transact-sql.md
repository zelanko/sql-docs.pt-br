---
title: OBJECTPROPERTYEX (Transact-SQL) | Microsoft Docs
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
- OBJECTPROPERTYEX
- OBJECTPROPERTYEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying schema-scoped object information
- viewing schema-scoped object information
- OBJECTPROPERTYEX function
- schema-scoped objects [SQL Server]
- objects [SQL Server], schema-scoped
ms.assetid: be36b3e3-3309-4332-bfb5-c7e9cf8dc8bd
caps.latest.revision: 76
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 73e4cbb26ea46753a79b9089acaaab7fe5d50e65
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="objectpropertyex-transact-sql"></a>OBJECTPROPERTYEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações sobre objetos no escopo do esquema no banco de dados atual. Para obter uma lista desses objetos, consulte [sys. Objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md). Não é possível usar a função OBJECTPROPERTYEX para objetos que não sejam do escopo de esquema, como gatilhos DDL (linguagem de definição de dados) e notificação de eventos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
OBJECTPROPERTYEX ( id , property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *id*  
 É uma expressão que representa a ID do objeto no banco de dados atual. *ID* é **int** e é considerado como um objeto no escopo do esquema no contexto do banco de dados atual.  
  
 *propriedade*  
 É uma expressão que contém as informações que serão retornadas para o objeto especificado pela identificação. O tipo de retorno é **sql_variant**. A tabela a seguir mostra o tipo de dados base para obter cada valor de propriedade.  
  
> [!NOTE]  
>  A menos que indicado em contrário, NULL é retornado quando *propriedade* não é um nome de propriedade válido, *id* não é uma ID de objeto válido, *id* é um tipo de objeto sem suporte especificado *propriedade*, ou o chamador não tem permissão para exibir os metadados do objeto.  
  
|Nome da propriedade|Tipo de objeto|Descrição e valores retornados|  
|-------------------|-----------------|-------------------------------------|  
|BaseType|Qualquer objeto no escopo do esquema|Identifica o tipo base do objeto. Quando o objeto especificado for SYNONYM, será retornado o tipo base do objeto subjacente.<br /><br /> Não nulo = Tipo de objeto<br /><br /> Tipo de dados base: **char(2)**|  
|CnstIsClustKey|Constraint|Restrição PRIMARY KEY com um índice clusterizado.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|CnstIsColumn|Constraint|Restrição CHECK, DEFAULT ou FOREIGN KEY em uma única coluna.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|CnstIsDeleteCascade|Constraint|Restrição FOREIGN KEY com a opção ON DELETE CASCADE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|CnstIsDisabled|Constraint|Restrição desabilitada.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|CnstIsNonclustKey|Constraint|Restrição PRIMARY KEY com um índice não clusterizado.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|CnstIsNotRepl|Constraint|A restrição é definida por meio das palavras-chave NOT FOR REPLICATION.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|CnstIsNotTrusted|Constraint|A restrição foi habilitada sem verificação das linhas existentes. Portanto, a restrição pode não ser válida para todas as linhas.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|CnstIsUpdateCascade|Constraint|Restrição FOREIGN KEY com a opção ON UPDATE CASCADE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsAfterTrigger|Gatilho|Gatilho AFTER.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsAnsiNullsOn|Função [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)], gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)], exibição|A configuração de ANSI_NULLS durante a criação.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsDeleteTrigger|Gatilho|Gatilho DELETE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsFirstDeleteTrigger|Gatilho|O primeiro gatilho acionado quando DELETE é executado na tabela.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsFirstInsertTrigger|Gatilho|O primeiro gatilho acionado quando INSERT é executado na tabela.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsFirstUpdateTrigger|Gatilho|O primeiro gatilho acionado quando UPADTE é executado na tabela.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsInsertTrigger|Gatilho|Gatilho INSERT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsInsteadOfTrigger|Gatilho|Gatilho INSTEAD OF.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsLastDeleteTrigger|Gatilho|Último gatilho acionado quando DELETE é executado na tabela.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsLastInsertTrigger|Gatilho|Último gatilho acionado quando INSERT é executado na tabela.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsLastUpdateTrigger|Gatilho|Último gatilho acionado quando UPDATE é executado na tabela.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsQuotedIdentOn|Função [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)], gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)], exibição|Configuração de QUOTED_IDENTIFIER na criação.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsStartup|Procedimento|Procedimento de inicialização.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsTriggerDisabled|Gatilho|Gatilho desabilitado.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsTriggerNotForRepl|Gatilho|Gatilho definido como NOT FOR REPLICATION.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsUpdateTrigger|Gatilho|Gatilho UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|ExecIsWithNativeCompilation|Procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)]|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> O procedimento é compilado nativamente.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|HasAfterTrigger|Tabela, exibição|A tabela ou exibição tem um gatilho AFTER.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|HasDeleteTrigger|Tabela, exibição|A tabela ou exibição tem um gatilho DELETE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|HasInsertTrigger|Tabela, exibição|A tabela ou exibição tem um gatilho INSERT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|HasInsteadOfTrigger|Tabela, exibição|A tabela ou exibição tem um gatilho INSTEAD OF.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|HasUpdateTrigger|Tabela, exibição|A tabela ou exibição tem um gatilho UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsAnsiNullsOn|Função [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)], tabela, gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)], exibição|Especifica a configuração da opção ANSI_NULLS para a tabela como ON, ou seja, todas as comparações com um valor nulo são avaliadas como UNKNOWN. Essa configuração se aplica a todas as expressões na definição da tabela, inclusive colunas computadas e restrições, enquanto a tabela existir.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsCheckCnst|Qualquer objeto no escopo do esquema|Restrição CHECK.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsConstraint|Qualquer objeto no escopo do esquema|Restrição.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsDefault|Qualquer objeto no escopo do esquema|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Padrão associado.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsDefaultCnst|Qualquer objeto no escopo do esquema|Restrição DEFAULT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsDeterministic|Funções escalares e com valor de tabela, exibição|A propriedade determinista da função ou exibição.<br /><br /> 1 = Determinista<br /><br /> 0 = Não determinista<br /><br /> Tipo de dados base: **int**|  
|IsEncrypted|Função [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)], tabela, gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)], exibição|Indica que o texto original da instrução de módulo foi convertido para um formato ofuscado. A saída do ofuscamento não é diretamente visível em quaisquer exibições de catálogo no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Os usuários que não tiverem acesso a tabelas do sistema ou arquivos do banco de dados não poderão recuperar o texto ofuscado. No entanto, o texto está disponível para os usuários que puderem acessar as tabelas do sistema sobre a [porta DAC](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) ou acessar diretamente os arquivos de banco de dados. Além disso, os usuários que podem anexar um depurador ao processo de servidor também podem recuperar o procedimento original da memória em tempo de execução.<br /><br /> 1 = Criptografado<br /><br /> 0 = não criptografado<br /><br /> Tipo de dados base: **int**|  
|IsExecuted|Qualquer objeto no escopo do esquema|Especifica que o objeto pode ser executado (exibição, procedimento, função ou gatilho).<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsExtendedProc|Qualquer objeto no escopo do esquema|Procedimento estendido.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsForeignKey|Qualquer objeto no escopo do esquema|Restrição FOREIGN KEY.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsIndexed|Tabela, exibição|Uma tabela ou exibição com um índice.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsIndexable|Tabela, exibição|Uma tabela ou exibição na qual um índice pode ser criado.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsInlineFunction|Função|Função embutida.<br /><br /> 1 = Função embutida<br /><br /> 0 = Função não embutida<br /><br /> Tipo de dados base: **int**|  
|IsMSShipped|Qualquer objeto no escopo do esquema|Um objeto criado durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsPrecise|Coluna computada, função, tipo definido pelo usuário, exibição|Indica se o objeto contém uma computação imprecisa, como operações de ponto flutuante.<br /><br /> 1 = Precisa<br /><br /> 0 = Imprecisa<br /><br /> Tipo de dados base: **int**|  
|IsPrimaryKey|Qualquer objeto no escopo do esquema|Restrição PRIMARY KEY.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsProcedure|Qualquer objeto no escopo do esquema|Procedimento.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsQuotedIdentOn|Restrição CHECK, definição DEFAULT, função [!INCLUDE[tsql](../../includes/tsql-md.md)], procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)], tabela, gatilho [!INCLUDE[tsql](../../includes/tsql-md.md)], exibição.|Especifica que a configuração do identificador entre aspas do objeto é ON, ou seja, aspas duplas delimitam identificadores em todas as expressões envolvidas na definição do objeto.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsQueue|Qualquer objeto no escopo do esquema|Fila do Service Broker<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsReplProc|Qualquer objeto no escopo do esquema|Procedimento de replicação.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsRule|Qualquer objeto no escopo do esquema|Regra associada.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsScalarFunction|Função|Função de valor escalar.<br /><br /> 1 = Função de valor escalar<br /><br /> 0 = Função com valor não escalar<br /><br /> Tipo de dados base: **int**|  
|IsSchemaBound|Função, Procedimento, exibição|Uma função associada a esquema ou exibição criada usando SCHEMABINDING.<br /><br /> 1 = Associada a esquema<br /><br /> 0 = Não associada a esquema<br /><br /> Tipo de dados base: **int**|  
|IsSystemTable|Table|Tabela do sistema.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsSystemVerified|Coluna computada, função, tipo definido pelo usuário, exibição|As propriedades de precisão e determinismo do objeto podem ser verificadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsTable|Table|Tabela.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsTableFunction|Função|Função com valor de tabela.<br /><br /> 1 = Função com valor de tabela<br /><br /> 0 = Função sem valor de tabela<br /><br /> Tipo de dados base: **int**|  
|IsTrigger|Qualquer objeto no escopo do esquema|Gatilho.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsUniqueCnst|Qualquer objeto no escopo do esquema|Restrição UNIQUE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsUserTable|Table|Tabela definida pelo usuário.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|IsView|Exibição|Exibição.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|OwnerId|Qualquer objeto no escopo do esquema|Proprietário do objeto.<br /><br /> **Observação:** proprietário do esquema não é necessariamente o proprietário do objeto. Por exemplo, os objetos filho (aqueles em que *parent_object_id* for não nulo) sempre retornará a mesma ID de proprietário que o pai.<br /><br /> Não nulo = A ID de usuário do banco de dados do proprietário do objeto.<br /><br /> NULL = Tipo de objeto sem suporte ou ID de objeto inválida.<br /><br /> Tipo de dados base: **int**|  
|SchemaId|Qualquer objeto no escopo do esquema|A ID do esquema associado ao objeto:<br /><br /> Não nulo = ID do esquema do objeto.<br /><br /> Tipo de dados base: **int**|  
|SystemDataAccess|Função, exibição|O objeto acessa dados do sistema, catálogos ou tabelas virtuais do sistema na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 0 = Nenhum<br /><br /> 1 = Leitura<br /><br /> Tipo de dados base: **int**|  
|TableDeleteTrigger|Table|A tabela tem um gatilho DELETE.<br /><br /> > 1 = ID do primeiro gatilho com o tipo especificado.<br /><br /> Tipo de dados base: **int**|  
|TableDeleteTriggerCount|Table|A tabela tem o número especificado de gatilhos DELETE.<br /><br /> Não nulo = Número de gatilhos DELETE<br /><br /> Tipo de dados base: **int**|  
|TableFullTextMergeStatus|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Se uma tabela que tem um índice de texto completo está atualmente em mesclagem.<br /><br /> 0 = A tabela não tem um índice de texto completo ou o índice de texto completo não está sendo mesclado.<br /><br /> 1 = O índice de texto completo está em mesclagem.|  
|TableFullTextBackgroundUpdateIndexOn|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> A tabela tem um índice de atualização em segundo plano de texto completo (controle de alterações automático) habilitado.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> Tipo de dados base: **int**|  
|TableFulltextCatalogId|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID do catálogo de texto completo no qual residem os dados do índice de texto completo para a tabela.<br /><br /> Diferente de zero = ID de catálogo de texto completo associado ao índice exclusivo que identifica as linhas em uma tabela indexada de texto completo.<br /><br /> 0 = A tabela não tem um índice de texto completo.<br /><br /> Tipo de dados base: **int**|  
|TableFullTextChangeTrackingOn|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> O controle de alterações de texto completo da tabela está habilitado.<br /><br /> 1 = TRUE<br /><br /> 0 = FALSE<br /><br /> Tipo de dados base: **int**|  
|TableFulltextDocsProcessed|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de linhas processadas desde o início da indexação de texto completo. Em uma tabela que está sendo indexada para pesquisa de texto completo, todas as colunas de uma linha são consideradas parte de um documento a ser indexado.<br /><br /> 0 = Nenhum rastreamento ativo ou indexação de texto completo está concluído.<br /><br /> > 0 = uma das opções a seguir (A ou B): A) o número de documentos processados pela inserção ou operações de atualização desde o início do completa, incremental ou manual população; de controle de alterações B) o número de linhas processadas pelo insert ou operações de atualização desde a habilitação do controle de alterações com população de índice de atualização em segundo plano, o esquema de índice de texto completo alterado, o catálogo de texto completo recriado ou a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reiniciado e assim por diante.<br /><br /> NULL = A tabela não tem um índice de texto completo.<br /><br /> Tipo de dados base: **int**<br /><br /> **Observação** essa propriedade não monitora nem conta linhas excluídas.|  
|TableFulltextFailCount|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> O número de linhas que a pesquisa de texto completo não indexou.<br /><br /> 0 = A população foi concluída.<br /><br /> > 0 = uma das opções a seguir (A ou B): A) o número de documentos que não foram indexados desde o início da atualização Manual, completo e Incremental population; de controle de alterações B) índice, o número de linhas que não foram indexados desde o início da população ou o reinício da população de atualização para o controle de alterações com o plano de fundo. A causa disso pode ter sido uma alteração de esquema, a reconstrução do catálogo, a reinicialização do servidor e assim por diante.<br /><br /> NULL = A tabela não tem um índice de texto completo.<br /><br /> Tipo de dados base: **int**|  
|TableFulltextItemCount|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Não nulo = Número de linhas com indexação de texto completo bem-sucedida.<br /><br /> NULL = A tabela não tem um índice de texto completo.<br /><br /> Tipo de dados base: **int**|  
|TableFulltextKeyColumn|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> ID da coluna associada ao índice exclusivo de coluna única que faz parte da definição de um índice de texto completo e de um índice semântico.<br /><br /> 0 = A tabela não tem um índice de texto completo.<br /><br /> Tipo de dados base: **int**|  
|TableFulltextPendingChanges|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Número de entradas de controle de alterações pendentes a serem processadas.<br /><br /> 0 = o controle de alterações não está habilitado.<br /><br /> NULL = A tabela não tem um índice de texto completo.<br /><br /> Tipo de dados base: **int**|  
|TableFulltextPopulateStatus|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 0 = Ocioso<br /><br /> 1 = População completa em andamento.<br /><br /> 2 = População incremental em andamento.<br /><br /> 3 = Propagação de alterações controladas em andamento.<br /><br /> 4 = Índice de atualização em segundo plano em andamento, bem como controle de alteração automática.<br /><br /> 5 = Indexação de texto completo acelerado ou pausado.<br /><br /> 6 = Ocorreu um erro. Examine o log de rastreamento para obter detalhes. Para obter mais informações, consulte o **solucionar problemas de erros em uma população de texto completo (rastreamento)** seção [popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).<br /><br /> Tipo de dados base: **int**|  
|TableFullTextSemanticExtraction|Table|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> A tabela está habilitada para indexação semântica.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasActiveFulltextIndex|Table|**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> A tabela tem um índice de texto completo ativo.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasCheckCnst|Table|A tabela tem uma restrição CHECK.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasClustIndex|Table|A tabela tem um índice clusterizado.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasDefaultCnst|Table|A tabela tem uma restrição DEFAULT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasDeleteTrigger|Table|A tabela tem um gatilho DELETE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasForeignKey|Table|A tabela tem uma restrição FOREIGN KEY.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasForeignRef|Table|A tabela é referenciada por uma restrição FOREIGN KEY.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasIdentity|Table|A tabela tem uma coluna de identidade.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasIndex|Table|A tabela tem um índice de qualquer tipo.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasInsertTrigger|Table|O objeto tem um gatilho INSERT.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasNonclustIndex|Table|A tabela tem um índice não clusterizado.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasPrimaryKey|Table|A tabela tem uma chave primária.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasRowGuidCol|Table|Tabela possui um ROWGUIDCOL para uma **uniqueidentifier** coluna.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasTextImage|Table|A tabela tem um **texto**, **ntext**, ou **imagem** coluna.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasTimestamp|Table|A tabela tem um **timestamp** coluna.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasUniqueCnst|Table|A tabela tem uma restrição UNIQUE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasUpdateTrigger|Table|O objeto tem um gatilho UPDATE.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableHasVarDecimalStorageFormat|Table|Tabela está habilitada para **vardecimal** o formato de armazenamento.<br /><br /> 1 = True<br /><br /> 0 = False|  
|TableInsertTrigger|Table|A tabela tem um gatilho INSERT.<br /><br /> > 1 = ID do primeiro gatilho com o tipo especificado.<br /><br /> Tipo de dados base: **int**|  
|TableInsertTriggerCount|Table|A tabela tem o número especificado de gatilhos INSERT.<br /><br /> >0 = O número de gatilhos INSERT.<br /><br /> Tipo de dados base: **int**|  
|TableIsFake|Table|A tabela não é real. Ela é materializada internamente sob demanda pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableIsLockedOnBulkLoad|Table|Tabela é bloqueada porque um **bcp** ou trabalho de inserção em MASSA.<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**|  
|TableIsMemoryOptimized|Table|**Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> A tabela tem otimização de memória<br /><br /> 1 = True<br /><br /> 0 = False<br /><br /> Tipo de dados base: **int**<br /><br /> Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).|  
|TableIsPinned|Table|A tabela está fixada para ser mantida no cache de dados.<br /><br /> 0 = False<br /><br /> Esse recurso não tem suporte no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores.|  
|TableTextInRowLimit|Table|A tabela tem uma opção text in row definida.<br /><br /> > 0 = Máximo de bytes permitidos para texto em linha.<br /><br /> 0 = se a opção text in row não estiver definida.<br /><br /> Tipo de dados base: **int**|  
|TableUpdateTrigger|Table|A tabela tem um gatilho UPDATE.<br /><br /> > 1 = ID do primeiro gatilho com o tipo especificado.<br /><br /> Tipo de dados base: **int**|  
|TableUpdateTriggerCount|Table|Tabela tem o número especificado de gatilhos UPDATE.<br /><br /> > 0 = O número de gatilhos UPDATE.<br /><br /> Tipo de dados base: **int**|  
|UserDataAccess|Função, exibição|Indica que o objeto acessa dados de usuário e tabelas de usuário na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = Leitura<br /><br /> 0 = Nenhum<br /><br /> Tipo de dados base: **int**|  
|TableHasColumnSet|Table|A tabela tem um conjunto de colunas.<br /><br /> 0 = False<br /><br /> 1 = True<br /><br /> Para obter mais informações, veja [Usar conjuntos de colunas](../../relational-databases/tables/use-column-sets.md).|  
|Cardinalidade|Tabela (sistema ou definido pelo usuário), exibição ou índice|**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> O número de linhas no objeto especificado.|  
|TableTemporalType|Table|**Aplica-se a**: do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> Especifica o tipo de tabela.<br /><br /> 0 = a tabela não temporal<br /><br /> 1 = a tabela de histórico para tabela com versão do sistema<br /><br /> 2 = a tabela temporal com versão do sistema|  
  
## <a name="return-types"></a>Tipos de retorno  
 **sql_variant**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que as funções internas emissoras de metadados, como OBJECTPROPERTYEX, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="remarks"></a>Comentários  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] supõe que *object_id* está no contexto do banco de dados atual. Uma consulta que faz referência a um *object_id* em outro banco de dados retornará NULL ou resultados incorretos. Por exemplo, na consulta a seguir, o contexto do banco de dados atual é o banco de dados mestre. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] tentará retornar o valor da propriedade especificado *object_id* no banco de dados em vez do banco de dados especificado na consulta. A consulta retorna resultados incorretos, pois o modo de exibição `vEmployee` não está no banco de dados mestre.  
  
```  
USE master;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID(N'AdventureWorks2012.HumanResources.vEmployee'), 'IsView');  
GO  
```  
  
 OBJECTPROPERTYEX (*view_i*d, 'IsIndexable') pode consumir recursos significativos do computador porque a avaliação da propriedade IsIndexable requer a análise da definição da exibição, normalização e otimização parcial. Embora a propriedade IsIndexable identifique tabelas ou exibições que podem ser indexadas, a criação atual do índice ainda poderá falhar se certos requisitos de chave de índice não forem atendidos. Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
 OBJECTPROPERTYEX (*table_id*, 'TableHasActiveFulltextIndex') retornará um valor de 1 (verdadeiro) quando pelo menos uma coluna de uma tabela for adicionada para indexação. A indexação de texto completo será ativada automaticamente para população assim que a primeira coluna for adicionada para indexação.  
  
 São aplicadas restrições de visibilidade dos metadados ao conjunto de resultados. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-finding-the-base-type-of-an-object"></a>A. Localizando o tipo base de um objeto  
 O exemplo a seguir cria um SYNONYM `MyEmployeeTable` para a tabela `Employee` do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], e, em seguida, retorna o tipo base do SYNONYM.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE SYNONYM MyEmployeeTable FOR HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX ( object_id(N'MyEmployeeTable'), N'BaseType')AS [Base Type];  
GO  
```  
  
 O conjunto de resultados mostra que o tipo base do objeto subjacente, a tabela `Employee`, é uma tabela de usuário.  
  
 `Base Type`  
  
 `--------`  
  
 `U`  
  
### <a name="b-returning-a-property-value"></a>B. Retornando um valor de propriedade  
 O exemplo a seguir retorna o número de gatilhos UPDATE na tabela especificada.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID(N'HumanResources.Employee'), N'TABLEUPDATETRIGGERCOUNT');  
GO  
  
```  
  
### <a name="c-finding-tables-that-have-a-foreign-key-constraint"></a>C. Localizando tabelas que possuem uma restrição FOREIGN KEY  
 O exemplo a seguir usa a propriedade `TableHasForeignKey` para retornar todas as tabelas que têm uma restrição FOREIGN KEY.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT name, object_id, schema_id, type_desc  
FROM sys.objects   
WHERE OBJECTPROPERTYEX(object_id, N'TableHasForeignKey') = 1  
ORDER BY name;  
GO  
  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="d-finding-the-base-type-of-an-object"></a>Unidade d: Localizando o tipo base de um objeto  
 O exemplo a seguir retorna o tipo base do `dbo.DimReseller` objeto.  
  
```  
-- Uses AdventureWorks  
  
SELECT OBJECTPROPERTYEX ( object_id(N'dbo.DimReseller'), N'BaseType')AS BaseType;  
```  
  
 O conjunto de resultados mostra que o tipo base do objeto subjacente, a tabela `dbo.DimReseller`, é uma tabela de usuário.  
  
```  
BaseType   
--------   
U   
```  
  
## <a name="see-also"></a>Consulte também  
 [Criar sinônimo &#40; Transact-SQL &#41;](../../t-sql/statements/create-synonym-transact-sql.md)   
 [Funções de metadados &#40; Transact-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [OBJECT_ID &#40; Transact-SQL &#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [Object_name &#40; Transact-SQL &#41;](../../t-sql/functions/object-name-transact-sql.md)   
 [sys. Objects &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [ALTER AUTHORIZATION &#40; Transact-SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [TYPEPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)  
  
  


