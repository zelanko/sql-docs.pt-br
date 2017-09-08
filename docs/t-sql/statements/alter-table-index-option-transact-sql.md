---
title: index_option (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- index_option
ms.assetid: 8a14f12d-2fbf-4036-b8b2-8db3354e0eb7
caps.latest.revision: 68
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 64f1d5cec0e74509e59491f50feec3be705badf2
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="alter-table-indexoption-transact-sql"></a>ALTER TABLE index_option (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica um conjunto de opções que podem ser aplicadas a um índice que faz parte de uma definição de restrição que é criada usando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
{   
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | SORT_IN_TEMPDB = { ON | OFF }   
  | ONLINE = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE |ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
      [ , ...n ] ) ]  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
<single_partition_rebuild__option> ::=  
{  
    SORT_IN_TEMPDB = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = {NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE } }  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                           ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
## <a name="arguments"></a>Argumentos  
 PAD_INDEX  **=**  {ON | **OFF** }  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o preenchimento do índice. O padrão é OFF.  
  
 ON  
 A porcentagem de espaço livre especificada por FILLFACTOR é aplicada às páginas de nível intermediário do índice.  
  
 DESATIVAR ou *fillfactor* não for especificado  
 As páginas de nível de intermediário são preenchidas até próximo de sua capacidade, deixando espaço suficiente para pelo menos uma linha do tamanho máximo que o índice pode ter, dado o conjunto de chaves em páginas intermediárias.  
  
 Fator de preenchimento  **=**  *fator de preenchimento*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica uma porcentagem que indica quanto [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve preencher o nível folha de cada página de índice durante a criação ou alteração do índice. O valor especificado deve ser um valor inteiro entre 1 e 100. O padrão é 0.  
  
> [!NOTE]  
>  Os valores 0 e 100 do fator de preenchimento são idênticos em todos os aspectos.  
  
 IGNORE_DUP_KEY  **=**  {ON | **OFF** }  
 Especifica a resposta de erro quando uma operação de inserção tenta inserir valores da chave duplicada em um índice exclusivo. A opção IGNORE_DUP_KEY aplica-se apenas a operações de inserção depois que o índice é criado ou recriado. A opção não tem nenhum efeito ao executar [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md), [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md), ou [atualização](../../t-sql/queries/update-transact-sql.md). O padrão é OFF.  
  
 ON  
 Uma mensagem de aviso será exibida quando valores de chave duplicados forem inseridos em um índice exclusivo. Ocorrerá falha somente nas linhas que violarem a restrição de exclusividade.  
  
 OFF  
 Ocorrerá uma mensagem de erro quando os valores de chave duplicados forem inseridos em um índice exclusivo. Toda a operação INSERT será revertida.  
  
 Ignore_dup_key não pode ser definida como ON para índices criados em um modo de exibição, índices não exclusivos, índices XML, índices espaciais e índices filtrados.  
  
 Para exibir IGNORE_DUP_KEY, use [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 Na sintaxe compatível com versões anteriores, WITH IGNORE_DUP_KEY é equivalente a WITH IGNORE_DUP_KEY = ON.  
  
 STATISTICS_NORECOMPUTE  **=**  {ON | **OFF** }  
 Especifica se as estatísticas são recalculadas. O padrão é OFF.  
  
 ON  
 As estatísticas desatualizadas não são recalculadas automaticamente.  
  
 OFF  
 A atualização automática de estatísticas está habilitada.  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** | OFF}  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica se bloqueios de linha são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de linha são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados.  
  
 OFF  
 Bloqueios de linha não são usados.  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** | OFF}  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica se bloqueios de página são permitidos. O padrão é ON.  
  
 ON  
 Bloqueios de página são permitidos ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados.  
  
 OFF  
 Bloqueios de página não são usados.  
  
 SORT_IN_TEMPDB  **=**  {ON | **OFF** }  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica se deseja armazenar os resultados de classificação em **tempdb**. O padrão é OFF.  
  
 ON  
 Os resultados intermediários de classificação que são usados para criar o índice são armazenados em **tempdb**. Isso pode reduzir o tempo necessário para criar um índice se **tempdb** está em um conjunto de discos diferente do banco de dados do usuário. Entretanto, isso aumenta o espaço em disco usado durante a criação do índice.  
  
 OFF  
 Os resultados intermediários de classificação são armazenados no mesmo banco de dados que o índice.  
  
 ON-LINE  **=**  {ON | **OFF** }  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica se as tabelas subjacentes e os índices associados estão disponíveis para consultas e modificação de dados durante a operação de índice. O padrão é OFF. REBUILD pode ser executado como uma operação ONLINE.  
  
> [!NOTE]  
>  Não podem ser criados índices de não cluster exclusivos on-line. Isso inclui índices criados devido a uma restrição UNIQUE ou PRIMARY KEY.  
  
 ON  
 Bloqueios de tabela de longa duração não são mantidos durante a operação do índice. Durante a fase principal da operação de índice, apenas um bloqueio IS (Tentativa Compartilhada) é mantido na tabela de origem. Ele permite o prosseguimento de consultas ou atualizações feitas na tabela e nos índices subjacentes. No início da operação, um bloqueio Compartilhado (S) é mantido no objeto de origem por um período muito curto. Ao término da operação, por um curto período de tempo, um bloqueio S (Compartilhado) será adquirido na origem se um índice não clusterizado estiver sendo criado; ou um bloqueio de modificação de esquema (SCH-M) será adquirido quando um índice clusterizado for criado ou descartado online e quando um índice clusterizado ou não clusterizado estiver sendo recriado. Embora os bloqueios de índice online sejam bloqueios de metadados curtos, especialmente o bloqueio Sch-M deve esperar que todas as transações de bloqueio sejam concluídas nessa tabela. Durante o tempo de espera, o bloqueio Sch-M bloqueia todas as transações restantes que esperam atrás desse bloqueio ao acessar a mesma tabela. Não será possível definir ONLINE como ON quando um índice estiver sendo criado em uma tabela temporária local.  
  
> [!NOTE]  
>  Recompilação de índice online pode definir o *low_priority_lock_wait* opções descritas posteriormente nesta seção. *low_priority_lock_wait* gerencia prioridade de bloqueio S e Sch-M durante a recompilação de índice online.  
  
 OFF  
 Os bloqueios de tabela são aplicados enquanto durar a operação de índice. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação. Uma operação de índice offline que cria, recria ou cancela um índice clusterizado ou recria ou cancela um índice não clusterizado, adquire um bloqueio de esquema de modificação (Sch-M) na tabela. Isso evita o acesso de todos os usuários à tabela subjacente enquanto durar a operação. Uma operação de índice offline que cria um índice não clusterizado adquire um bloqueio Compartilhado (S) na tabela. Isso impede atualizações na tabela subjacente, mas permite operações de leitura, como instruções SELECT.  
  
 Para obter mais informações, consulte [como funcionam as operações de índice Online](../../relational-databases/indexes/how-online-index-operations-work.md).  
  
> [!NOTE]  
>  As operações de índice online não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 MAXDOP  **=**  *max_degree_of_parallelism*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Substitui o **grau máximo de paralelismo** opção de configuração para a duração da operação de índice. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP para limitar o número de processadores usados em uma execução de plano paralelo. O máximo é de 64 processadores.  
  
 *max_degree_of_parallelism* pode ser:  
  
 1  
 Suprime a geração de plano paralelo.  
  
 \>1  
 Restringe o número máximo de processadores usados em uma operação de índice paralela ao número especificado.  
  
 0 (padrão)  
 Usa o número real de processadores, ou menos, com base na carga de trabalho atual do sistema.  
  
 Para obter mais informações, consulte [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!NOTE]  
>  Operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 DATA_COMPRESSION  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica a opção de compactação de dados para a tabela especificada, o número de partição ou o intervalo de partições. As opções são as seguintes:  
  
 NONE  
 A tabela ou as partições especificadas não são compactadas. Aplica-se somente a tabelas rowstore; não se aplica a tabelas columnstore.  
  
 ROW  
 A tabela ou as partições especificadas são compactadas usando a compactação de linha. Aplica-se somente a tabelas rowstore; não se aplica a tabelas columnstore.  
  
 PAGE  
 A tabela ou as partições especificadas são compactadas usando a compactação de página. Aplica-se somente a tabelas rowstore; não se aplica a tabelas columnstore.  
  
 COLUMNSTORE  
 **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se somente a tabelas columnstore. COLUMNSTORE especifica a descompactação de uma partição compactada com a opção COLUMNSTORE_ARCHIVE. Quando os dados forem restaurados, eles continuarão sendo compactados através da compactação columnstore usada em todas as tabelas columnstore.  
  
 COLUMNSTORE_ARCHIVE  
 **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se a tabelas columnstore, que são armazenadas com um índice columnstore clusterizado. COLUMNSTORE_ARCHIVE compactará ainda mais a partição especificada para um tamanho menor. Isso pode ser usado para fins de arquivamento, ou em outras situações que exijam menos armazenamento e possam dispensar mais tempo para armazenamento e recuperação  
  
 Para obter mais informações sobre compactação, consulte [compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
EM partições **(** { \<partition_number_expression > | \<intervalo >} [ **,**...  *n*  ] **)** **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica as partições às quais se aplica a configuração DATA_COMPRESSION. Se a tabela não for particionada, o argumento ON PARTITIONS gerará um erro. Se a cláusula ON PARTITIONS não for fornecida, a opção DATA_COMPRESSION será aplicada a todas as partições de uma tabela particionada.  
  
\<partition_number_expression > pode ser especificado das seguintes maneiras:  
  
-   Forneça o número de uma partição, por exemplo: ON PARTITIONS (2).  
  
-   Forneça os números de várias partições individuais separados por vírgulas, por exemplo: ON PARTITIONS (1, 5).  
  
-   Forneça os intervalos e as partições individuais, por exemplo: ON PARTITIONS (2, 4, 6 TO 8).  
  
 \<Range > pode ser especificado como números de partição separados pela palavra TO, por exemplo: ON PARTITIONS (6 TO 8).  
  
 Para definir tipos diferentes de compactação de dados para partições diferentes, especifique a opção DATA_COMPRESSION mais de uma vez, por exemplo:  
  
```  
--For rowstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
  
--For columnstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = COLUMNSTORE ON PARTITIONS (1, 3, 5),   
DATA_COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (2, 4, 6 TO 8)  
)  
```  
  
**\<single_partition_rebuild__option >**  
 Na maioria das vezes, a reconstrução de um índice reconstruirá todas as partições de um índice particionado. As opções a seguir, quando aplicadas a uma única partição, não recriarão todas as partições.  
  
-   SORT_IN_TEMPDB  
  
-   MAXDOP  
  
-   DATA_COMPRESSION  
  
**low_priority_lock_wait**  
 **Aplica-se a**: do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Um **SWITCH** ou recompilação de índice online for concluído, assim como não há operações de bloqueio para essa tabela. *WAIT_AT_LOW_PRIORITY* indica que, se o **SWITCH** ou operação de recompilação de índice online não pode ser concluída imediatamente, ela aguardará. A operação manterá os bloqueios de baixa prioridade, permitindo que outras operações que mantêm bloqueios que estão em conflito com a instrução DDL continuem. A omissão de **WAIT AT LOW PRIORITY** opção é equivalente a `WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`.  
  
MAX_DURATION = *tempo* [**minutos** ]  
 O tempo (um valor inteiro especificado em minutos) que o **SWITCH** ou bloqueio de recompilação de índice online que deve ser adquirido esperará ao executar o comando DDL. A opção SWITCH ou a operação de recompilação de índice online tenta ser concluída imediatamente. Se a operação está bloqueada para o **MAX_DURATION** de tempo, uma da **ABORT_AFTER_WAIT** ações serão executadas. **MAX_DURATION** hora é sempre em minutos e a palavra **minutos** pode ser omitido.  
  
ABOUT_AFTER_WAIT = [**NONE** | **SELF** | **BLOQUEADORES** }]  
 Nenhuma  
 Continua a **SWITCH** ou operação de recompilação sem alterar a prioridade de bloqueio (usando a prioridade normal) de índice online.  
  
SELF  
 Fecha o **SWITCH** ou operação de DDL de recompilação de índice online em execução sem realizar nenhuma ação.  
  
BLOCKERS  
 Elimina todas as transações de usuário que bloqueiam atualmente a **SWITCH** ou operação DDL de recompilação, para que possa continuar a operação de índice online.  
 BLOQUEADORES requer o **ALTER ANY CONNECTION** permissão.  
  
## <a name="remarks"></a>Comentários  
 Para obter uma descrição completa das opções de índice, consulte [CREATE INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_constraint &#40; Transact-SQL &#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)   
 [computed_column_definition &#40; Transact-SQL &#41;](../../t-sql/statements/alter-table-computed-column-definition-transact-sql.md)   
 [table_constraint &#40; Transact-SQL &#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  
  
 

