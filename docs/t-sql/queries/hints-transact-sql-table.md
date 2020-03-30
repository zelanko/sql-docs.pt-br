---
title: Dicas de tabela (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TABLE_HINT_TSQL
- Table Hint
dev_langs:
- TSQL
helpviewer_keywords:
- SERIALIZABLE table hint
- UPDLOCK table hint
- HOLDLOCK table hint
- TABLOCKX table hint
- READUNCOMMITTED table hint
- hints [SQL Server], tables
- READCOMMITTEDLOCK table hint
- FORCESCAN table hint
- ROWLOCK table hint
- XLOCK table hint
- NOLOCK table hint
- READPAST table hint
- NOWAIT table hint
- FORCESEEK table hint
- table hints [SQL Server]
- TABLOCK table hint
- REPEATABLEREAD table hint
- READ COMMITTED table hint
- NOEXPAND table hint
- PAGLOCK table hint
ms.assetid: 8bf1316f-c0ef-49d0-90a7-3946bc8e7a89
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d5675f7c62ce43a9e41770075cd4a97253ea051e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73981759"
---
# <a name="hints-transact-sql---table"></a>Dicas (Transact-SQL) – tabela
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  As dicas de tabela substituem o comportamento padrão do otimizador de consulta durante a instrução DML (linguagem de manipulação de dados) ao especificar um método de bloqueio, um ou mais índices, uma operação de processamento de consulta, como uma verificação de tabela ou busca de índice, ou outras opções. As dicas da tabela são especificadas na cláusula FROM da instrução DML e afetam apenas a tabela ou exibição referenciada nessa cláusula.  
  
> [!CAUTION]  
>  Como o otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente seleciona o melhor plano de execução para uma consulta, é recomendável que desenvolvedores e administradores de banco de dados experientes usem as dicas apenas como um último recurso.  
  
 **Aplica-se a:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
WITH  ( <table_hint> [ [, ]...n ] )  
  
<table_hint> ::=   
[ NOEXPAND ] {   
    INDEX  ( index_value [ ,...n ] )   
  | INDEX =  ( index_value )      
  | FORCESEEK [( index_value ( index_column_name  [ ,... ] ) ) ]  
  | FORCESCAN  
  | FORCESEEK  
  | HOLDLOCK   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | READUNCOMMITTED   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT   
  | SPATIAL_WINDOW_MAX_CELLS = integer  
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK   
}   
  
<table_hint_limited> ::=  
{  
    KEEPIDENTITY   
  | KEEPDEFAULTS   
  | HOLDLOCK   
  | IGNORE_CONSTRAINTS   
  | IGNORE_TRIGGERS   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT   
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK   
}   
```  
  
## <a name="arguments"></a>Argumentos  
WITH **(** \<table_hint> **)** [ [ **,** ]...*n* ]  
Com algumas exceções, há suporte para dicas de tabela na cláusula FROM somente quando elas são especificadas com a palavra-chave WITH. Dicas de tabela também devem ser especificadas com parênteses.  
  
> [!IMPORTANT]  
> A omissão da palavra-chave WITH é um recurso preterido: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
As seguintes dicas de tabelas são permitidas com ou sem a palavra-chave WITH: NOLOCK, READUNCOMMITTED, UPDLOCK, REPEATABLEREAD, SERIALIZABLE, READCOMMITTED, TABLOCK, TABLOCKX, PAGLOCK, ROWLOCK, NOWAIT, READPAST, XLOCK, SNAPSHOT e NOEXPAND. Quando essas dicas de tabela forem especificadas sem a palavra-chave WITH, as dicas deverão ser especificadas sozinhas. Por exemplo:  
  
```sql  
FROM t (TABLOCK)  
```  
  
Quando especificada com outra opção, a dica deverá ser especificada com a palavra-chave WITH:  
  
```sql  
FROM t WITH (TABLOCK, INDEX(myindex))  
```  
  
É recomendável usar vírgulas entre dicas de tabela.  
  
> [!IMPORTANT]  
>  A separação de dicas com espaços em vez de vírgulas não é mais um recurso aceito: [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
NOEXPAND  
Especifica que qualquer exibição indexada não será expandida para acessar tabelas subjacentes quando o otimizador de consulta processar a consulta. O otimizador de consulta trata a exibição como uma tabela com índice clusterizado. NOEXPAND aplica-se apenas a exibições indexadas. Para obter mais informações, confira [Usando NOEXPAND](#using-noexpand).  
  
INDEX  **(** _index\_value_ [ **,** ... _n_ ] ) | INDEX =  ( _index\_value_ **)**  
A sintaxe de INDEX() especifica os nomes ou as IDs de um ou mais índices a serem usados pelo otimizador de consulta ao processar a instrução. A alternativa INDEX = sintaxe especifica um único valor de índice. Apenas uma dica de índice por tabela pode ser especificada.  
  
Se existir um índice clusterizado, INDEX(0) forçará uma verificação de índice clusterizado e INDEX(1) forçará uma verificação ou busca de índice clusterizado. Na ausência de índices clusterizados, INDEX(0) forçará uma verificação de tabela e INDEX(1) será interpretado como um erro.  
  
 Se forem usados vários índices em uma única lista de índices, as duplicatas serão ignoradas e os demais índices listados serão usados para recuperar as linhas da tabela. A ordem dos índices na dica de índice é importante. Uma dica de vários índices também impõe o uso de AND de índice e o otimizador de consulta aplicará tantas condições quantas forem possíveis em cada índice acessado. Se a coleção de índices com dica não incluir todas as colunas referidas pela consulta, uma busca será executada para recuperar as colunas restantes depois que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] recuperar todas as colunas indexadas.  
  
> [!NOTE]  
> Quando uma dica de índice que faz referência a vários índices for usada na tabela de fatos em uma junção em estrela, o otimizador ignorará a dica de índice e retornará uma mensagem de aviso. Além disso, o uso de OR de índice não é permitido em uma tabela com uma dica de índice especificada.  
  
 O número máximo de índices na dica de tabela é de 250 índices não clusterizados.  
  
KEEPIDENTITY  
É aplicável apenas em uma instrução INSERT quando a opção BULK é usada com [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  
  
 Especifica que o valor, ou valores, de identidade no arquivo de dados importado deve ser usado para a coluna de identidade. Se KEPIDENTITY não estiver especificado, os valores de identidade dessa coluna serão verificados, mas não importados, e o otimizador de consulta atribuirá automaticamente os valores com base nos valores de semente e de incremento especificados durante a criação da tabela.  
  
> [!IMPORTANT]  
> Se o arquivo de dados não contiver valores para a coluna de identidade na tabela ou na exibição e a coluna de identidade não for a última coluna da tabela, a coluna de identidade deverá ser ignorada. Para obter mais informações, confira [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md). Se uma coluna de identidade for ignorada com êxito, o otimizador de consulta atribuirá valores exclusivos automaticamente para a coluna de identidade nas linhas da tabela importada.  
  
Para obter um exemplo que usa essa dica em uma `INSERT ... SELECT * FROM OPENROWSET(BULK...)` instrução, confira [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md).  
  
Para obter informações de como verificar o valor de identidade de uma tabela, confira [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md).  
  
KEEPDEFAULTS  
É aplicável apenas em uma instrução INSERT quando a opção BULK é usada com [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  
  
Especifica a inserção de um valor padrão da coluna de tabela, se houver algum, em vez de NULL, se o registro de dados não tiver um valor para a coluna.  
  
Para obter um exemplo que usa essa dica em uma instrução INSERT... SELECT * FROM OPENROWSET(BULK...), confira [Manter valores nulos ou usar os valores padrão durante a importação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md).  
  
FORCESEEK [ **(** _index\_value_ **(** _index\_column\_name_ [ **,** ... _n_ ] **))** ]  
Especifica que o otimizador de consulta usará apenas uma operação de busca de índice como o caminho de acesso aos dados na tabela ou exibição. 

> [!NOTE]
> A partir do [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SP1, parâmetros de índice também podem ser especificados. Nesse caso, o otimizador de consulta considera apenas as operações de busca de índice através do índice especificado, usando pelo menos as colunas de índice especificadas.  
  
 *index_value*  
 É o valor do nome ou ID do índice. A ID do índice 0 (heap) não pode ser especificada. Para retornar a ID ou o nome do índice, confira a exibição de catálogo **sys.indexes**.  
  
 *index_column_name*  
 É o nome da coluna de índice a ser incluída na operação de busca. Especificar FORCESEEK com parâmetros de índice é semelhante a usar FORCESEEK com uma dica INDEX. Entretanto, você pode adquirir maior controle sobre o caminho de acesso usado pelo otimizador de consulta especificando o índice a ser pesquisado e as colunas de índice a serem consideradas na operação de busca. O otimizador pode considerar colunas adicionais, caso necessário. Por exemplo, se um índice não clusterizado for especificado, o otimizador poderá optar por usar colunas de chave de índice clusterizado além das colunas especificadas.  
  
A dica FORCESEEK pode ser especificada das formas a seguir.  
  
|Sintaxe|Exemplo|Descrição|  
|------------|-------------|-----------------|  
|Sem um índice ou dica INDEX|`FROM dbo.MyTable WITH (FORCESEEK)`|O otimizador de consulta considera apenas as operações de busca de índice para acessar a tabela ou exibição através de qualquer índice relevante.|  
|Combinado com uma dica INDEX.|`FROM dbo.MyTable WITH (FORCESEEK, INDEX (MyIndex))`|O otimizador de consulta considera apenas as operações de busca de índice para acessar a tabela ou exibição através do índice especificado.|  
|Parametrizado especificando um índice e colunas do índice|`FROM dbo.MyTable WITH (FORCESEEK (MyIndex (col1, col2, col3)))`|O otimizador de consulta considera apenas as operações de busca de índice para acessar a tabela ou exibição através do índice especificado, usando pelo menos as colunas de índice especificadas.|  
  
Ao usar a dica FORCESEEK (com ou sem parâmetros de índice), considere as diretrizes a seguir:  
-   A dica pode ser especificada como uma dica de tabela ou como uma dica de consulta. Para obter mais informações sobre dicas de consulta, confira [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
-   Para aplicar FORCESEEK a uma exibição indexada, a dica NOEXPAND também deve ser especificada.  
-   A dica pode ser aplicada no máximo uma vez por tabela ou exibição.  
-   A dica não pode ser especificada para uma fonte de dados remotos. O erro 7377 é retornado quando FORCESEEK é especificado com uma dica de índice e o erro 8180 é retornado quando FORCESEEK é usado sem uma dica de índice.  
-   Se FORCESEEK impedir a localização de um plano, o erro 8622 será retornado.  
  
Quando FORCESEEK for especificado com parâmetros de índice, as diretrizes e restrições a seguir se aplicarão:  
-   A dica não pode ser especificada para uma tabela que é o destino de uma instrução INSERT, UPDATE ou DELETE.  
-   A dica não pode ser especificada em combinação com uma dica INDEX ou outra dica FORCESEEK.  
-   Pelo menos uma coluna deve ser especificada e ela deve ser a coluna de chave à esquerda.  
-   Colunas de índice adicionais podem ser especificadas; entretanto, colunas de chave não podem ser ignoradas. Por exemplo, se o índice especificado contiver as colunas de chave `a`, `b` e `c`, a sintaxe válida incluirá `FORCESEEK (MyIndex (a))` e `FORCESEEK (MyIndex (a, b)`. A sintaxe inválida incluiria `FORCESEEK (MyIndex (c))` e `FORCESEEK (MyIndex (a, c)`.  
-   A ordem de nomes de coluna especificada na dica deve corresponder à ordem das colunas no índice referenciado.  
-   As colunas que não constam na definição de chave de índice não podem ser especificadas. Por exemplo, em um índice não clusterizado, apenas as colunas de chave de índice definidas podem ser especificadas. As colunas de chave clusterizadas que são incluídas automaticamente no índice não podem ser especificadas, mas podem ser usadas pelo otimizador.  
-   Um índice columnstore xVelocity com otimização de memória não pode ser especificado como parâmetro de índice. O erro 366 é retornado.  
-   A modificação da definição de índice (por exemplo, adicionando ou removendo colunas) talvez exija modificações nas consultas que fazem referência a esse índice.  
-   A dica impede que o otimizador considere índices espaciais ou XML na tabela.  
-   A dica não pode ser especificada em combinação com a dica FORCESCAN.  
-   Para índices particionados, a coluna de particionamento implicitamente adicionada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode ser especificada na dica FORCESEEK.  
  
> [!CAUTION]  
> A especificação de FORCESEEK com parâmetros limita o número de planos que podem ser considerados pelo otimizador mais do que a especificação de FORCESEEK sem parâmetros. Isso pode causar um erro `Plan cannot be generated` em mais casos. Em uma versão futura, as modificações internas no otimizador de consulta poderão permitir que mais planos sejam considerados.  
  
FORCESCAN **aplica-se ao**: [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SP1 e posterior.
Especifica que o otimizador de consulta usará apenas uma operação de verificação de índice como o caminho de acesso na tabela ou exibição referenciada. A dica FORCESCAN pode ser útil em consultas nas quais o otimizador menospreza o número de linhas afetadas e escolhe uma operação de busca em vez de uma operação de verificação. Quando isso ocorre, a quantidade de memória concedida para a operação é muito baixa e o desempenho da consulta é afetado.  
  
FORCESCAN pode ser especificado com ou sem uma dica INDEX. Quando combinado com uma dica de índice, (`INDEX = index_name, FORCESCAN`), o otimizador de consulta considera apenas os caminhos de acesso de verificação através do índice especificado ao acessar a tabela referenciada. FORCESCAN pode ser especificado com a dica de índice INDEX(0) para forçar uma operação de verificação de tabela na tabela base.  
  
Para tabelas e índices particionados, FORCESCAN é aplicado após a eliminação de partições através da avaliação de predicado de consulta. Isso significa que a verificação é aplicada apenas às partições restantes e não à tabela inteira.  
  
A dica FORCESCAN tem as restrições a seguir:  
-   A dica não pode ser especificada para uma tabela que é o destino de uma instrução INSERT, UPDATE ou DELETE.  
-   A dica não pode ser usada com mais de uma dica de índice.  
-   A dica impede que o otimizador considere índices espaciais ou XML na tabela.  
-   A dica não pode ser especificada para uma fonte de dados remotos.  
-   A dica não pode ser especificada em combinação com a dica FORCESEEK.  
  
HOLDLOCK  
É equivalente a SERIALIZABLE. Para obter mais informações, consulte SERIALIZABLE posteriormente neste tópico. HOLDLOCK aplica-se apenas à tabela ou exibição para a qual está especificada e somente durante a transação definida pela instrução usada. HOLDLOCK não pode ser usada em uma instrução SELECT que inclua a opção FOR BROWSE.  
  
IGNORE_CONSTRAINTS  
É aplicável apenas em uma instrução INSERT quando a opção BULK é usada com [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  
  
Especifica que qualquer restrição da tabela é ignorada pela operação de importação em massa. Por padrão, INSERT verifica [Restrições exclusivas e restrições de verificação](../../relational-databases/tables/unique-constraints-and-check-constraints.md) e [Restrições primárias e de chave estrangeira](../../relational-databases/tables/primary-and-foreign-key-constraints.md). Quando a opção IGNORE_CONSTRAINTS for especificada para uma operação de importação em massa, INSERT deverá ignorar essas restrições em uma tabela de destino. Observe que não é possível desabilitar restrições UNIQUE, PRIMARY KEY ou NOT NULL.  
  
Convém desabilitar restrições CHECK e FOREIGN KEY se os dados de entrada contiverem linhas que violam restrições. Ao desabilitar as restrições CHECK e FOREIGN KEY, será possível importar os dados e usar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para limpar os dados.  
  
No entanto, quando as restrições FOREIGN KEY e CHECK são ignoradas, cada restrição ignorada na tabela é marcada como **is_not_trusted** na exibição de catálogo [sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md) ou [sys.foreign_keys](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md) após a operação. Em algum ponto, verifique as restrições de toda a tabela. Se a tabela não estiver vazia antes da operação de importação em massa, o custo de revalidação da restrição poderá exceder o custo da aplicação das restrições CHECK e FOREIGN KEY aos dados incrementais.  
  
IGNORE_TRIGGERS  
É aplicável apenas em uma instrução INSERT quando a opção BULK é usada com [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md).  
  
Especifica que qualquer gatilho definido na tabela será ignorado pela operação de importação em massa. Por padrão, INSERT aplica gatilhos.  
  
Use IGNORE_TRIGGERS apenas se o aplicativo não depender de nenhum gatilho e se for importante maximizar o desempenho.  
  
NOLOCK  
É equivalente a READUNCOMMITTED. Para obter mais informações, consulte READUNCOMMITTED mais adiante neste tópico.  
  
> [!NOTE]  
> Para instruções UPDATE ou DELETE: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
NOWAIT  
Instrui o [!INCLUDE[ssDE](../../includes/ssde-md.md)] a retornar uma mensagem assim que um bloqueio for encontrado na tabela. NOWAIT é equivalente a especificar SET LOCK_TIMEOUT 0 para uma tabela específica. A dica NOWAIT não funciona quando a dica TABLOCK também é incluída. Para terminar uma consulta sem aguardar ao usar a dica TABLOCK, preceda a consulta por `SETLOCK_TIMEOUT 0;`.  
  
PAGLOCK  
Usa bloqueios de página onde bloqueios individuais são usados normalmente em linhas ou chaves ou onde um único bloqueio de tabela é usado normalmente. Por padrão, usa o modo de bloqueio adequado para a operação. Quando especificados em transações que operam no nível de isolamento de SNAPSHOT, os bloqueios de página não são usados a menos que PAGLOCK seja combinado com outras dicas de tabela que requerem bloqueios, como UPDLOCK e HOLDLOCK.  
  
READCOMMITTED  
Especifica que as operações de leitura obedecem a regras do nível de isolamento READ COMMITTED usando bloqueio ou controle de versão de linha. Se a opção READ_COMMITTED_SNAPSHOT do banco de dados for OFF, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] irá adquirir bloqueios compartilhados conforme os dados forem lidos e liberará esses bloqueios quando a operação de leitura estiver concluída. Se a opção READ_COMMITTED_SNAPSHOT do banco de dados for ON, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não adquirirá bloqueios e usará controle de versão de linha. Para obter mais informações sobre os níveis de isolamento, confira [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
> [!NOTE]  
> Para instruções UPDATE ou DELETE: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
READCOMMITTEDLOCK  
Especifica que operações de leitura obedecem às regras do nível de isolamento READ COMMITTED usando bloqueio. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] adquire bloqueios compartilhados conforme os dados são lidos e libera esses bloqueios quando a operação de leitura é concluída, independentemente da configuração da opção READ_COMMITTED_SNAPSHOT do banco de dados. Para obter mais informações sobre os níveis de isolamento, confira [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md). Esta dica não pode ser especificada na tabela de destino de uma instrução INSERT; o erro 4140 é retornado.  
  
READPAST  
Especifica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não lê linhas bloqueadas por outras transações. Quando READPAST é especificado, os bloqueios no nível da linha são ignorados, mas os bloqueios no nível da página não são. Ou seja, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] ignorará as linhas em vez de bloquear a transação atual até que os bloqueios sejam liberados. Por exemplo, suponhamos que a tabela `T1` contenha uma única coluna de inteiros com os valores 1, 2, 3, 4, 5. Se a transação A alterar o valor de 3 para 8, mas ainda não foi confirmada, SELECT * FROM T1 (READPAST) produzirá os valores 1, 2, 4, 5. READPAST é usado principalmente para reduzir a contenção de bloqueio ao implementar uma fila de trabalho que usa uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um queue reader usando READPAST ignora entradas da fila bloqueadas por outras transações, passando para a próxima entrada da fila, sem precisar esperar até que outras transações liberem seus bloqueios.  
  
READPAST pode ser especificado para qualquer tabela referenciada em uma instrução UPDATE ou DELETE e em qualquer tabela referenciada em uma cláusula FROM. Quando especificado em uma instrução UPDATE, READPAST será aplicado apenas ao ler dados para identificar quais registros atualizar, independentemente de onde na instrução ele foi especificado. READPAST não pode ser especificado para tabelas na cláusula INTO de uma instrução INSERT. Operações de atualização ou de exclusão que usam READPAST podem ser bloqueadas ao ler chaves estrangeiras ou exibições indexadas ou ao modificar índices secundários.  
  
READPAST pode ser especificado apenas em transações que operam nos níveis de isolamento READ COMMITTED ou REPEATABLE READ. Quando especificado em transações que operam no nível de isolamento SNAPSHOT, READPAST deverá ser combinado com outras dicas de tabela que requerem bloqueios, como UPDLOCK e HOLDLOCK.  
  
A dica de tabela READPAST não pode ser especificada quando a opção do banco de dados READ_COMMITTED_SNAPSHOT for definida como ON e qualquer uma das condições a seguir forem verdadeiras:  
-   O nível de isolamento da transação da sessão é READ COMMITTED.  
-   A dica de tabela READCOMMITTED também é especificada na consulta.  
  
Para especificar a dica READPAST nesses casos, remova a dica de tabela READCOMMITTED, se ela estiver presente, e inclua a dica de tabela READCOMMITTEDLOCK na consulta.  
  
READUNCOMMITTED  
Especifica que leituras sujas são permitidas. Nenhum bloqueio compartilhado é emitido para impedir que outras transações modifiquem dados lidos pela transação atual, e bloqueios exclusivos definidos por outras transações não impedem que a transação atual leia os dados bloqueados. Permitir leituras sujas pode provocar maior simultaneidade, mas à custa da leitura de modificações de dados que, em seguida, serão revertidas por outras transações. Isso pode gerar erros para sua transação, apresentar aos usuários dados que nunca foram confirmados ou fazer com que os usuários vejam registros duplicados (ou nenhum).  
  
Dicas de READUNCOMMITTED e de NOLOCK aplicam-se apenas a bloqueios de dados. Todas as consultas, inclusive aquelas com dicas de READUNCOMMITTED e NOLOCK, adquirem bloqueios Sch-S (estabilidade de esquema) durante a compilação e a execução. Por causa disso, as consultas são bloqueadas quando uma transação simultânea mantém um bloqueio Sch-M (modificação de esquema) na tabela. Por exemplo, uma operação DDL (Linguagem de Definição de Dados) adquire um bloqueio Sch-M antes de modificar as informações do esquema da tabela. Todas as consultas simultâneas, inclusive aquelas executadas com dicas de READUNCOMMITTED ou NOLOCK, serão bloqueadas ao tentar adquirir um bloqueio Sch-S. Da mesma forma, uma consulta que mantém um bloqueio Sch-S bloqueará uma transação simultânea que tentar adquirir um bloqueio Sch-M.  
  
READUNCOMMITTED e NOLOCK não podem ser especificados para tabelas modificadas por operações de inserção, atualização ou exclusão. O otimizador de consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignora as dicas de READUNCOMMITTED e NOLOCK na cláusula FROM que se aplicam à tabela de destino de uma instrução UPDATE ou DELETE.  
  
> [!NOTE]  
> O suporte ao uso de dicas de READUNCOMMITTED e NOLOCK na cláusula FROM que se aplicam à tabela de destino de uma instrução UPDATE ou DELETE será eliminado em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar essas dicas nesse contexto em desenvolvimentos novos e planeje modificar aplicativos que as usam atualmente.  
  
É possível minimizar a contenção de bloqueio ao proteger transações de leituras sujas de modificações de dados não confirmadas usando:  
-   O nível de isolamento READ COMMITTED com a opção de banco de dados READ_COMMITTED_SNAPSHOT definida como ON.  
-   O nível de isolamento SNAPSHOT.  
  
Para obter mais informações sobre os níveis de isolamento, confira [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
> [!NOTE]  
> Se você receber a mensagem de erro 601 ao especificar READUNCOMMITTED, resolva-a como se fosse um erro de deadlock (1205) e envie novamente a instrução.  
  
REPEATABLEREAD  
Especifica que um exame é executado com a mesma semântica de bloqueio de uma transação que está sendo executada no nível de isolamento SERIALIZABLE. Para obter mais informações sobre os níveis de isolamento, confira [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
ROWLOCK  
Especifica que bloqueios de linha serão usados quando os bloqueios de página ou de tabela forem usados normalmente. Quando especificados em transações que operam no nível de isolamento SNAPSHOT, os bloqueios de linha não serão usados a menos que ROWLOCK seja combinado com outras dicas de tabela que requerem bloqueios, como UPDLOCK e HOLDLOCK.  
  
SERIALIZABLE  
É equivalente a HOLDLOCK. Torna bloqueios compartilhados mais restritivos ao mantê-los até que uma transação seja concluída, em vez de liberar o bloqueio compartilhado assim que a tabela ou página de dados requerida não seja mais necessária, quer a transação tenha sido concluída ou não. A verificação é executada com a mesma semântica da transação que está sendo executada no nível de isolamento SERIALIZABLE. Para obter mais informações sobre os níveis de isolamento, confira [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
SNAPSHOT  
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior. 
  
A tabela com otimização de memória é acessada no isolamento SNAPSHOT. O SNAPSHOT pode ser usado apenas com tabelas com otimização de memória (não com tabelas com base em disco). Para obter mais informações, confira [Introdução às tabelas com otimização de memória](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md).  
  
```sql 
SELECT * FROM dbo.Customers AS c   
WITH (SNAPSHOT)   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id=oh.customer_id;  
```  
  
SPATIAL_WINDOW_MAX_CELLS = *integer*  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
Especifica o número máximo de células para usar para fazer um mosaico de geometria ou objeto de geografia. *number* é um valor entre 1 e 8192.  
  
Esta opção permite ajustar o tempo de execução de consulta ajustando o intercâmbio entre o tempo de execução de filtro primário e secundário. Um número maior reduz o tempo de execução de filtro secundário, mas aumenta hora de filtro de execução primária e um número menor diminui tempo de execução de filtro primário, mas aumenta a execução de filtro secundária. Para dados espaciais mais densos, um número mais alto deve gerar um tempo de execução mais rápido dando uma aproximação melhor com o filtro primário e reduzindo o tempo de execução de filtro secundário. Para dados mais esparsos, um número inferior diminuirá o tempo de execução de filtro primário.  
  
 Essa opção funciona para mosaicos de grade manuais e automáticos.  
  
TABLOCK  
Especifica que o bloqueio adquirido seja aplicado no nível de tabela. O tipo de bloqueio que é adquirido depende da instrução que está sendo executada. Por exemplo, uma instrução SELECT pode adquirir um bloqueio compartilhado. Ao especificar TABLOCK, o bloqueio compartilhado é aplicado à tabela inteira, e não no nível de linha ou página. Se HOLDLOCK também for especificado, o bloqueio de tabela será mantido até o final da transação.  
  
Ao importar dados para um heap usando a instrução \<target_table> SELECT \<columns> FROM \<source_table>, você pode habilitar o registro em log e o bloqueio otimizados da instrução, especificando a dica TABLOCK para a tabela de destino. Além disso, o modelo de recuperação do banco de dados deve ser definido como simples ou bulk-logged. Para obter mais informações, consulte [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
Quando usado com o provedor de conjuntos de linhas em massa [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) para importar dados em uma tabela, TABLOCK permite que vários clientes carreguem dados simultaneamente na tabela de destino com o registro em log e o bloqueio otimizados. Para obter mais informações, confira [Pré-requisitos para registro em log mínimo em importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md).  
  
TABLOCKX  
Especifica que um bloqueio exclusivo será usado na tabela.  
  
UPDLOCK  
Especifica que bloqueios de atualização serão usados e mantidos até que a transação seja concluída. UPDLOCK utiliza bloqueios de atualização apenas em operações de leitura no nível de linha ou de página. Se UPDLOCK for combinado com TABLOCK, ou se um bloqueio em nível de tabela for usado por outro motivo, um bloqueio (X) exclusivo será usado.  
  
Quando UPDLOCK é especificado, as dicas em nível de isolamento READCOMMITTED e READCOMMITTEDLOCK são ignoradas. Por exemplo, se o nível de isolamento da sessão for definido como SERIALIZABLE e uma consulta especificar (UPDLOCK, READCOMMITTED), a dica READCOMMITTED será ignorada e a transação será executada usando o nível de isolamento SERIALIZABLE.  
  
XLOCK  
Especifica que bloqueios exclusivos serão usados e mantidos até que a transação seja concluída. Se especificados com ROWLOCK, PAGLOCK ou TABLOCK, os bloqueios exclusivos serão aplicados ao nível adequado de granularidade.  
  
## <a name="remarks"></a>Comentários  
As dicas de tabela serão ignoradas se a tabela não for acessada pelo plano de consulta. Isso pode ser provocado porque o otimizador opta por não acessar a tabela ou porque uma exibição indexada é acessada. No último caso, o acesso a uma exibição indexada pode ser evitado pela dica de consulta OPTION (EXPAND VIEWS).  
  
Todas as dicas de bloqueio são propagadas para todas as tabelas e exibições que são acessadas pelo plano de consulta, incluindo tabelas e exibições referenciadas em uma exibição. Além disso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa os testes de consistência de bloqueio correspondentes.  
  
Dicas de bloqueio ROWLOCK, UPDLOCK e XLOCK que adquirem bloqueios em nível de linha colocam bloqueios em chaves de índice em vez das linhas de dados reais. Por exemplo, se uma tabela tiver um índice não clusterizado e uma instrução SELECT que usa uma dica de bloqueio for tratada por um índice de cobertura, um bloqueio será adquirido na chave do índice de cobertura em vez de na linha de dados da tabela base.  
  
Se a tabela contiver colunas computadas por expressões ou funções que acessam colunas em outras tabelas, as dicas de tabela não serão usadas nessas tabelas e não serão propagadas. Por exemplo, uma dica de tabela NOLOCK é especificada em uma tabela na consulta. Essa tabela contém colunas computadas que são computadas por uma combinação de expressões e funções que acessam colunas de outras tabelas. As tabelas referenciadas pelas expressões e funções não usam a dica de tabela NOLOCK quando acessadas.  
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite mais de uma dica de tabela de cada um dos seguintes grupos para cada tabela na cláusula FROM:  
-   Dicas de granularidade: PAGLOCK, NOLOCK, READCOMMITTEDLOCK, ROWLOCK, TABLOCK ou TABLOCKX.  
-   Dicas de nível de isolamento: HOLDLOCK, NOLOCK, READCOMMITTED, REPEATABLEREAD, SERIALIZABLE.  
  
## <a name="filtered-index-hints"></a>Dicas de índice filtrado  
 Um índice filtrado pode ser usado como uma dica de tabela, mas fará com que o otimizador de consulta gere o erro 8622 se ele não cobrir todas as linhas selecionadas pela consulta. O seguinte exemplo é uma dica de índice filtrado inválida. O exemplo cria o índice filtrado `FIBillOfMaterialsWithComponentID` e, em seguida, usa-o como uma dica de índice para uma instrução SELECT. O predicado do índice filtrado inclui linhas de dados para ComponentIDs 533, 324 e 753. O predicado da consulta também inclui linhas de dados para os ComponentIDs 533, 324 e 753, mas estende o conjunto de resultados para incluir os ComponentIDs 855 e 924 que não estão no índice filtrado. Portanto, o otimizador de consulta não pode usar a dica de índice filtrado e gera o erro 8622. Para saber mais, confira [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
```sql  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithComponentID'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithComponentID  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithComponentID"  
    ON Production.BillOfMaterials (ComponentID, StartDate, EndDate)  
    WHERE ComponentID IN (533, 324, 753);  
GO  
SELECT StartDate, ComponentID FROM Production.BillOfMaterials  
    WITH( INDEX (FIBillOfMaterialsWithComponentID) )  
    WHERE ComponentID in (533, 324, 753, 855, 924);  
GO  
```  
  
O otimizador de consulta não considerará uma dica de índice se as opções SET não tiverem os valores necessários para índices filtrados. Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="using-noexpand"></a>Usando NOEXPAND  
NOEXPAND aplica-se somente a *exibições indexadas*. Uma exibição indexada é uma exibição com um índice clusterizado exclusivo criado nela. Se uma consulta tiver referências a colunas presentes em uma exibição indexada e em tabelas base, e o otimizador de consulta determinar que o uso da exibição indexada oferece o melhor método para a execução da consulta, o otimizador de consulta usará o índice na exibição. Essa funcionalidade é chamada de *correspondência de exibição indexada*. Antes do [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1, o uso automático de uma exibição indexada pelo otimizador de consulta era compatível apenas em edições específicas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
No entanto, para que o otimizador considere exibições indexadas para correspondência ou uso de uma exibição indexada que é referenciada com a dica NOEXPAND, as seguintes opções SET devem ser definidas como ON.  
 
> [!NOTE]  
> O [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] é compatível com o automático de exibições indexadas sem especificar a dica NOEXPAND.
  
||||  
|-|-|-|  
|ANSI_NULLS|ANSI_WARNINGS|CONCAT_NULL_YIELDS_NULL|  
|ANSI_PADDING|ARITHABORT<sup>1</sup>|QUOTED_IDENTIFIER|  
  
 <sup>1</sup> ARITHABORT é definido implicitamente como ON quando ANSI_WARNINGS é definido como ON. Portanto, você não precisa ajustar essa configuração manualmente.  
  
 Além disso, a opção NUMERIC_ROUNDABORT deve ser definida como OFF.  
  
 Para forçar o otimizador a usar um índice para uma exibição indexada, especifique a opção NOEXPAND. Essa dica poderá ser usada apenas se a exibição também estiver nomeada na consulta. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não fornece uma dica para forçar o uso de uma exibição indexada específica em uma consulta que não nomeie a exibição diretamente na cláusula FROM. No entanto, o otimizador de consulta considera o uso de exibições indexadas, mesmo que elas não sejam referenciadas diretamente na consulta. O SQL Server apenas criará automaticamente as estatísticas em uma exibição indexada quando uma dica de tabela NOEXPAND for usada. A omissão dessa dica pode resultar em avisos de plano de execução sobre as estatísticas ausentes que não podem ser resolvidas com a criação manual de estatísticas. Durante a otimização da consulta, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usará as estatísticas de exibição que foram criadas automaticamente ou manualmente quando a consulta referenciar a exibição diretamente e a dica NOEXPAND for usada.    
  
## <a name="using-a-table-hint-as-a-query-hint"></a>Usando uma dica de tabela como uma dica de consulta  
 As *dicas de tabela* também podem ser especificadas como dicas de consulta usando a cláusula OPTION (TABLE HINT). É recomendável usar uma dica de tabela como uma dica de consulta apenas no contexto de um [guia de plano](../../relational-databases/performance/plan-guides.md). Para consultas ad hoc, especifique essas dicas apenas como dicas de tabela. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="permissions"></a>Permissões  
 As dicas KEEPIDENTITY, IGNORE_CONSTRAINTS e IGNORE_TRIGGERS requerem permissões ALTER na tabela.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-the-tablock-hint-to-specify-a-locking-method"></a>a. Usando a dica TABLOCK para especificar um método de bloqueio  
 O seguinte exemplo especifica que um bloqueio compartilhado será usado na tabela `Production.Product` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] e mantido até o término da instrução UPDATE.  
  
```sql  
UPDATE Production.Product  
WITH (TABLOCK)  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE 'BK-%';  
GO  
```  
  
### <a name="b-using-the-forceseek-hint-to-specify-an-index-seek-operation"></a>B. Usando a dica FORCESEEK para especificar uma operação de busca de índice  
 O exemplo a seguir usa a dica FORCESEEK sem especificar um índice para forçar o otimizador de consulta a executar uma operação de busca de índice na tabela `Sales.SalesOrderDetail` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql
SELECT *  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d WITH (FORCESEEK)  
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);  
GO  
  
```  
  
 O exemplo a seguir usa a dica FORCESEEK com um índice para forçar o otimizador de consulta a executar uma operação de busca de índice no índice e na coluna de índice especificados.  
  
```sql  
SELECT h.SalesOrderID, h.TotalDue, d.OrderQty  
FROM Sales.SalesOrderHeader AS h  
    INNER JOIN Sales.SalesOrderDetail AS d   
    WITH (FORCESEEK (PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID (SalesOrderID)))   
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);   
GO  
  
```  
  
### <a name="c-using-the-forcescan-hint-to-specify-an-index-scan-operation"></a>C. Usando a dica FORCESCAN para especificar uma operação de verificação de índice  
 O exemplo a seguir usa a dica FORCESCAN para forçar o otimizador de consultas a executar uma operação de verificação na tabela `Sales.SalesOrderDetail` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
SELECT h.SalesOrderID, h.TotalDue, d.OrderQty  
FROM Sales.SalesOrderHeader AS h  
    INNER JOIN Sales.SalesOrderDetail AS d   
    WITH (FORCESCAN)   
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [Query Hints &#40;Transact-SQL&#41; [Dicas de consulta (Transact-SQL)]](../../t-sql/queries/hints-transact-sql-query.md)  
  
  
