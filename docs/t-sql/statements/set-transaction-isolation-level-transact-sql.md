---
description: SET TRANSACTION ISOLATION LEVEL (Transact-SQL)
title: SET TRANSACTION ISOLATION LEVEL (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- LEVEL
- LEVEL_TSQL
- SET TRANSACTION ISOLATION LEVEL
- ISOLATION
- ISOLATION_TSQL
- SET_TRANSACTION_ISOLATION_LEVEL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET TRANSACTION ISOLATION LEVEL statement
- row versioning [SQL Server], isolation levels
- TRANSACTION ISOLATION LEVEL option
- isolation levels [SQL Server], setting
- locking [SQL Server], isolation levels
- transactions [SQL Server], isolation levels
ms.assetid: 016fb05e-a702-484b-bd2a-a6eabd0d76fd
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 977ebc69d15e88de11e5906bb1e283f7e73d072a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89540541"
---
# <a name="set-transaction-isolation-level-transact-sql"></a>SET TRANSACTION ISOLATION LEVEL (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]


Controla o comportamento de bloqueio e do controle de versão de linha das instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] emitidas por uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for SQL Server and Azure SQL Database
  
SET TRANSACTION ISOLATION LEVEL
    { READ UNCOMMITTED
    | READ COMMITTED
    | REPEATABLE READ
    | SNAPSHOT
    | SERIALIZABLE
    }
```

```syntaxsql
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse
  
SET TRANSACTION ISOLATION LEVEL READ UNCOMMITTED
```

>[!NOTE]
> O SQL Data Warehouse implementa transações ACID. O nível de isolamento do suporte transacional usa como padrão READ UNCOMMITTED.  Você pode alterá-lo para to READ COMMITTED SNAPSHOT ISOLATION selecionando ON na opção de banco de dados READ_COMMITTED_SNAPSHOT para um banco de dados do usuário quando conectado ao banco de dados mestre.  Uma vez habilitada, todas as transações neste banco de dados são executadas em READ COMMITTED SNAPSHOT ISOLATION e a configuração READ UNCOMMITTED no nível da sessão não será respeitada. Confira [Opções ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md) para detalhes.  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 READ UNCOMMITTED  
 Especifica que as instruções podem ler linhas que foram modificadas por outras transações, mas que ainda não foram confirmadas.  
  
 Transações em execução em nível READ UNCOMMITTED não emitem bloqueios compartilhados para impedir que outras transações modifiquem os dados lidos pela transação atual. Transações READ UNCOMMITTED também não são bloqueadas por bloqueios exclusivos que impediriam a transação atual de ler linhas que foram modificadas, mas não confirmadas, por outras transações. Quando essa opção está definida, é possível ler modificações não confirmadas, chamadas de leituras sujas. Os valores nos dados podem ser alterados e linhas podem aparecer ou desaparecer do conjunto de dados antes do término da transação. Essa opção tem o mesmo efeito de definir NOLOCK em todas as tabelas em todas as instruções SELECT em uma transação. Esse é o menos restritivo dos níveis de isolamento.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você também pode minimizar a contenção de bloqueios e, ao mesmo tempo, proteger as transações contra leituras sujas de modificações de dados não confirmadas, usando:  
  
-   O nível de isolamento READ COMMITTED com a opção de banco de dados READ_COMMITTED_SNAPSHOT definida como ON.  
  
-   O nível de isolamento SNAPSHOT. Para obter mais informações sobre isolamento de instantâneo, confira [Isolamento de instantâneo no SQL Server](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/snapshot-isolation-in-sql-server). 
  
 READ COMMITTED  
 Especifica que as instruções não podem ler dados que foram modificados, mas que ainda não foram confirmados por outras transações. Isso impede leituras sujas. Os dados podem ser alterados por outras transações entre instruções individuais dentro da transação atual, resultando em leituras não repetíveis ou dados fantasmas. Essa é a opção padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O comportamento de READ COMMITTED depende da configuração da opção de banco de dados READ_COMMITTED_SNAPSHOT:  
  
-   Se READ_COMMITTED_SNAPSHOT estiver definido como OFF (o padrão no SQL Server), o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usará bloqueios compartilhados para impedir que outras transações modifiquem linhas enquanto a transação atual estiver executando uma operação de leitura. Os bloqueios compartilhados também bloqueiam a instrução de ler linhas modificadas por outras transações até que a outra transação seja concluída. O tipo de bloqueio compartilhado determina quando ele será liberado. Os bloqueios de linha são liberados antes que a próxima linha seja processada. Os bloqueios de página são liberados quando a próxima página é lida e bloqueios de tabela são liberados quando a instrução é finalizada.  
  
-   Se READ_COMMITTED_SNAPSHOT estiver definido como ON (o padrão no Banco de Dados SQL do Azure), o [!INCLUDE[ssDE](../../includes/ssde-md.md)] usará o controle de versão de linhas para apresentar a cada instrução um instantâneo transacionalmente consistente dos dados como estavam no início da instrução. Não são usados bloqueios para proteger os dados contra atualizações efetuadas por outras transações.

> [!IMPORTANT]  
> Escolhendo um nível de isolamento da transação não afeta os bloqueios obtidos para proteger as modificações de dados. Uma transação sempre obtém um bloqueio exclusivo em quaisquer dados que modifica e mantém tal bloqueio até que a transação seja concluída, sem considerar o conjunto de níveis de isolamento para a transação em questão. Além disso, uma atualização feita no nível de isolamento READ_COMMITTED usa bloqueios de atualização nas linhas de dados selecionadas, enquanto uma atualização feita no nível de isolamento SNAPSHOT usa versões de linha para selecionar as linhas a serem atualizadas. Para operações de leitura, níveis de isolamento da transação definem principalmente o nível de proteção dos efeitos das modificações feitas por outras transações. Confira o [Guia de controle de versão de linha e bloqueio de transação](https://docs.microsoft.com/sql/relational-databases/sql-server-transaction-locking-and-row-versioning-guide) para obter mais informações.

> [!NOTE]  
>  O isolamento de instantâneo oferece suporte a dados FILESTREAM. No modo de isolamento de instantâneos, os dados FILESTREAM lidos por qualquer instrução em uma transação serão a versão transacionalmente consistente dos dados que existiam no início da transação.  
  
 Quando a opção de banco de dados READ_COMMITTED_SNAPSHOT for ON, você poderá usar a dica de tabela READCOMMITTEDLOCK para solicitar bloqueio compartilhado, em vez do controle de versão de linhas, para instruções individuais em transações em execução no nível de isolamento READ COMMITTED.  
  
> [!NOTE]  
>  Quando a opção READ_COMMITTED_SNAPSHOT está definida, apenas a conexão que executa o comando ALTER DATABASE é permitida no banco de dados. Não deve haver nenhuma outra conexão aberta no banco de dados até que ALTER DATABASE esteja concluído. O banco de dados não precisa estar no modo do usuário único.  
  
 REPEATABLE READ  
 Especifica que as instruções não podem ler dados que foram modificados, mas que ainda não foram confirmados por outras transações e que nenhuma outra transação pode modificar dados que foram lidos pela transação atual até que a transação atual seja concluída.  
  
 Os bloqueios compartilhados são colocados em todos os dados lidos por cada instrução na transação, sendo mantidos até que a transação seja concluída. Isso impede que outras transações modifiquem qualquer linha que tenha sido lida pela transação atual. Outras transações podem inserir novas linhas que correspondam às condições de pesquisa das instruções emitidas pela transação atual. Então, se a transação atual tentar a instrução novamente, ela recuperará as novas linhas, o que resultará em leituras fantasmas. Como os bloqueios compartilhados são mantidos até o término da transação, em vez de serem liberados ao final de cada instrução, a simultaneidade é menor que o nível de isolamento READ COMMITTED padrão. Use essa opção apenas quando necessário.  
  
 SNAPSHOT  
 Especifica que os dados lidos por qualquer instrução em uma transação serão a versão transacionalmente consistente que existia no início da transação. A transação pode reconhecer apenas modificações de dados que estavam confirmadas antes do início da transação. Modificações de dados efetuadas por outras transações após o início da transação atual não são visíveis para as instruções em execução na transação atual. O efeito é como se as instruções em uma transação obtivessem um instantâneo dos dados confirmados conforme existiam no início da transação.  
  
 Exceto quando um banco de dados está sendo recuperado, as transações SNAPSHOT não exigeem bloqueios ao ler dados. Transações SNAPSHOT que leem dados não bloqueiam outras transações de gravar dados. Transações que gravam dados não bloqueiam transações SNAPSHOT de ler dados.  
  
 Durante a fase de reversão de uma recuperação de banco de dados, as transações SNAPSHOT solicitarão um bloqueio se houver uma tentativa de ler dados que se encontram bloqueados por outra transação que está sendo revertida. A transação SNAPSHOT será bloqueada até que aquela transação seja revertida. O bloqueio será liberado tão logo seja concedido.  
  
 A opção de banco de dados ALLOW_SNAPSHOT_ISOLATION deve ser definida como ON para que uma transação que usa o nível de isolamento SNAPSHOT seja iniciada. Se uma transação que usa o nível de isolamento SNAPSHOT acessar dados em vários bancos de dados, ALLOW_SNAPSHOT_ISOLATION deve ser definida como ON em cada banco de dados.  
  
 Uma transação iniciada com outro nível de isolamento não pode ser definida com o nível de isolamento SNAPSHOT; isso causaria a anulação da transação. Se uma transação for iniciada no nível de isolamento SNAPSHOT, você poderá alterar seu nível de isolamento e retorná-la para o SNAPSHOT. Uma transação é iniciada na primeira vez em que ela acessa dados.  
  
 Uma transação em execução sob o nível de isolamento SNAPSHOT pode exibir as alterações feitas por essa transação. Por exemplo, se a transação executar um UPDATE em uma tabela e, em seguida, emitir uma instrução SELECT na mesma tabela, os dados modificados serão incluídos no conjunto de resultados.  
  
> [!NOTE]  
>  No modo de isolamento de instantâneos, os dados FILESTREAM lidos por qualquer instrução em uma transação serão a versão transacionalmente consistente dos dados que existiam no início da transação, não da instrução.  
  
 SERIALIZABLE  
 Especifica o seguinte:  
  
-   As instruções não podem ler dados que foram modificados, mas que ainda não foram confirmados por outras transações.  
  
-   Nenhuma outra transação pode modificar dados lidos pela transação atual até que a transação atual seja concluída.  
  
-   Outras transações não podem inserir linhas novas com valores chave que estejam no intervalo de chaves lido por qualquer instrução da transação atual até que esta seja concluída.  
  
 Bloqueios de intervalo são colocados no intervalo de valores chave que corresponde às condições de pesquisa de cada instrução executada em uma transação. Isso bloqueia que outras transações atualizem ou insiram qualquer linha que seja qualificada para qualquer uma das instruções executadas pela transação atual. Isto significa que, se qualquer uma das instruções de uma transação for executada uma segunda vez, ela lerá o mesmo conjunto de linhas. Os bloqueios de intervalo são mantidos até que a transação seja concluída. Esse é o mais restritivo dos níveis de isolamento, pois ele bloqueia intervalos de chaves inteiros até que a transação seja concluída. Como a simultaneidade é menor, use essa opção apenas quando necessário. Essa opção tem o mesmo efeito de definir HOLDLOCK em todas as tabelas em todas as instruções SELECT de uma transação.  
  
## <a name="remarks"></a>Comentários  
 Apenas uma única opção de nível de isolamento pode ser definida por vez, permanecendo definida para aquela conexão até que seja explicitamente alterada. Todas as operações de leitura executadas na transação operam sob as regras do nível de isolamento especificado, a menos que uma dica de tabela na cláusula FROM de uma instrução especifique comportamento de bloqueio ou controle de versão diferente para uma tabela.  
  
 Os níveis de isolamento da transação definem o tipo de bloqueio adquirido em operações de leitura. Bloqueios compartilhados adquiridos para READ COMMITTED ou REPEATABLE READ geralmente são bloqueios de linha, embora os bloqueios de linha possam ser escalados para bloqueios de página ou de tabela se um número significativo de linhas em uma página ou tabela forem referenciadas pela leitura. Se uma linha for modificada pela transação depois de ter sido lida, a transação irá adquirir um bloqueio exclusivo para proteger essa linha, sendo mantido até que a transação seja concluída. Por exemplo, se uma transação REPEATABLE READ tiver um bloqueio compartilhado em uma linha e a transação modificar essa linha, o bloqueio de linha compartilhado será convertido em bloqueio de linha exclusivo.  
  
 A não ser por uma exceção, é possível alternar de um nível de isolamento para outro durante uma transação. A exceção ocorre ao alterar de qualquer nível de isolamento para o isolamento SNAPSHOT. Isso faz com que a transação falhe e seja revertida. Porém, é possível alterar uma transação iniciada em isolamento SNAPSHOT para qualquer outro nível de isolamento.  
  
 Quando você altera uma transação de um nível de isolamento para outro, os recursos lidos após a alteração são protegidos de acordo com as regras do novo nível. Recursos lidos antes da alteração continuam sendo protegidos de acordo com as regras do nível anterior. Por exemplo, se uma transação mudar de READ COMMITTED para SERIALIZABLE, os bloqueios compartilhados adquiridos após a alteração serão, nesse caso, mantidos até o término da transação.  
  
 Se você emitir SET TRANSACTION ISOLATION LEVEL em um procedimento armazenado ou em um gatilho, quando o controle retornar para o objeto retornar, o nível de isolamento será redefinido como o nível que estava em vigor quando o objeto foi invocado. Por exemplo, se você definir REPEATABLE READ em um lote e o lote chamar um procedimento armazenado que define o nível de isolamento como SERIALIZABLE, a configuração do nível de isolamento será revertida para REPEATABLE READ quando o procedimento armazenado retornar o controle para o lote.  
  
> [!NOTE]  
>  Funções e tipos CLR (Common Language Runtime) definidos pelo usuário não podem executar SET TRANSACTION ISOLATION LEVEL. Porém, você pode substituir o nível de isolamento com o uso de uma dica de tabela. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Quando você usa sp_bindsession para associar duas sessões, cada sessão retém sua configuração de nível de isolamento. O uso de SET TRANSACTION ISOLATION LEVEL para alterar a configuração do nível de isolamento de uma sessão não afeta a configuração de nenhuma outra sessão associada a ela.  
  
 SET TRANSACTION ISOLATION LEVEL entra em vigor na execução ou em tempo de execução, e não em tempo de análise.  
  
 Operações de carregamento em massa otimizadas em heaps bloqueiam consultas executadas com os seguintes níveis de isolamento:  
  
-   SNAPSHOT  
  
-   READ UNCOMMITTED  
  
-   READ COMMITTED usando controle de versão de linha  
  
 De modo oposto, consultas executadas com esses níveis de isolamento bloqueiam operações de carregamento em massa otimizados em heaps. Para obter mais informações sobre as operações de carregamento em massa, veja [Importação e exportação de dados em massa &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 Bancos de dados habilitados por FILESTREAM dão suporte aos seguintes níveis de isolamento de transação.  
  
|Nível de isolamento|Acesso ao Transact SQL|Acesso ao sistema de arquivos|  
|---------------------|-------------------------|------------------------|  
|Leitura não confirmada|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Sem suporte|  
|Leitura confirmada|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|Leitura repetida|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Sem suporte|  
|Serializável|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Sem suporte|  
|Instantâneo de leitura confirmada|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
|Instantâneo|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define o `TRANSACTION ISOLATION LEVEL` da sessão. Para cada instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantém todos os bloqueios compartilhados até o término da transação.  
  
```sql
USE AdventureWorks2012;  
GO  
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;  
GO  
BEGIN TRANSACTION;  
GO  
SELECT *   
    FROM HumanResources.EmployeePayHistory;  
GO  
SELECT *   
    FROM HumanResources.Department;  
GO  
COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [DBCC USEROPTIONS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [Dicas de tabela &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md)  
  
  
