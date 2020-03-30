---
title: 'Planejar a adoção de OLTP in-memory '
ms.custom: seo-dt-2019
ms.date: 01/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 041b428f-781d-4628-9f34-4d697894e61e
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f899a8fc1ad5a316784a83cb13f29acb84a01b2b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74412549"
---
# <a name="plan-your-adoption-of-in-memory-oltp-features-in-sql-server"></a>Planejar a adoção de recursos de OLTP in-memory no SQL Server
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


Este artigo descreve as formas como a adoção de recursos in-memory afeta outros aspectos do seu sistema empresarial.



## <a name="a-adoption-of-in-memory-oltp-features"></a>a. Adoção de recursos do OLTP in-memory


As subseções a seguir discutem fatores que você deve considerar ao planejar adotar e implementar recursos in-memory. Muitas informações explicativas estão disponíveis em:

- [Usar o OLTP in-memory para melhorar o desempenho do aplicativo no Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-in-memory-oltp-migration/)



### <a name="a1-prerequisites"></a>A.1 Pré-requisitos

Um pré-requisito para usar os recursos in-memory pode envolver a edição ou a camada de serviço do produto SQL. Para esse e outros pré-requisitos, consulte:

- [Requisitos para usar tabelas com otimização de memória](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)
    - [Edições e componentes do SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
    - [Recomendações de tipo de preço do Banco de Dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-service-tier-advisor/)


### <a name="a2-forecast-the-amount-of-active-memory"></a>A. 2 Prever a quantidade de memória ativa

O sistema tem memória ativa suficiente para dar suporte a uma nova tabela com otimização de memória?

#### <a name="microsoft-sql-server"></a>Microsoft SQL Server

Uma tabela com otimização de memória que contém 200 GB de dados requer mais de 200 GB de memória ativa dedicados a seu suporte. Antes de implementar uma tabela com otimização de memória que contém uma grande quantidade de dados, você precisa prever a quantidade de memória ativa adicional que talvez seja necessário adicionar ao computador servidor. Para obter diretrizes para fazer uma estimativa, consulte:

- [Estimar requisitos de memória para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)

#### <a name="azure-sql-database"></a>Banco de Dados SQL do Azure

Para um banco de dados hospedado no serviço de nuvem do Banco de Dados SQL do Azure, a camada de serviço escolhida afeta a quantidade de memória ativa que o banco de dados pode consumir. Você deve se planejar para monitorar o uso de memória do banco de dados usando um alerta. Para obter detalhes, confira:

- Examine os limites de armazenamento de OLTP in-memory para seu [Tipo de preço](https://docs.microsoft.com/azure/sql-database/sql-database-purchase-models)
- [Monitorar o armazenamento no OLTP in-memory](https://azure.microsoft.com/documentation/articles/sql-database-in-memory-oltp-monitoring/)

#### <a name="memory-optimized-table-variables"></a>Variáveis de tabela com otimização de memória

Uma variável de tabela declarada como com otimização de memória às vezes é preferível a uma #TempTable tradicional que reside no banco de dados **tempdb** . Essas variáveis de tabela podem fornecer ganhos de desempenho significativos sem usar uma quantidade significativa de memória ativa.

### <a name="a3-table-must-be-offline-to-convert-to-memory-optimized"></a>A.3 A tabela deve estar offline para ser convertida para uma tabela com otimização de memória

Algumas funcionalidades de ALTER TABLE estão disponíveis para tabelas com otimização de memória. Mas você não pode emitir uma instrução ALTER TABLE para converter uma tabela baseada em disco em uma tabela com otimização de memória. Em vez disso, você deve usar um conjunto de etapas mais manuais. A seguir, temos várias maneiras de converter a tabela baseada em disco em uma tabela com otimização de memória.

#### <a name="manual-scripting"></a>Script manual

Uma maneira de converter a tabela baseada em disco em uma tabela com otimização de memória é codificar você mesmo as etapas necessárias de Transact-SQL.


1. Suspenda a atividade do aplicativo.

2. Faça um backup completo.

3. Renomeie a tabela baseada em disco.

4. Emita uma instrução CREATE TABLE para criar a nova tabela com otimização de memória.

5. INSIRA na tabela com otimização de memória com uma SUBSELEÇÃO da tabela baseada em disco.

6. DESCARTE a tabela baseada em disco.

7. Faça outro backup completo.

8. Retome a atividade do aplicativo.


#### <a name="memory-optimization-advisor"></a>Orientador de otimização da memória

A ferramenta Orientador de Otimização de Memória pode gerar um script para ajudar a implementar a conversão de uma tabela baseada em disco para uma tabela com otimização de memória. A ferramenta é instalada como parte do SSDT (SQL Server Data Tools).

- [Orientador de otimização da memória](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md)
- [Baixar o SQL Server Data Tools (SSDT)](../../ssdt/download-sql-server-data-tools-ssdt.md)


#### <a name="dacpac-file"></a>Arquivo .dacpac

Você pode atualizar seu banco de dados localmente usando um arquivo. dacpac, gerenciado pelo SSDT. No SSDT, você pode especificar alterações no esquema codificado no arquivo .dacpac.

Você trabalha com arquivos .dacpac no contexto de um projeto do Visual Studio do tipo *Banco de Dados*.

- [Aplicativos da camada de dados](../../relational-databases/data-tier-applications/data-tier-applications.md) e arquivos .dacpac



### <a name="a4-guidance-for-whether-in-memory-oltp-features-are-right-for-your-application"></a>A.4 Diretrizes sobre a adequação dos recursos de OLTP in-memory para seu aplicativo

Para obter diretrizes sobre se os recursos de OLTP in-memory podem melhorar o desempenho de seu aplicativo específico, consulte:

- [OLTP na memória (otimização na memória)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)



## <a name="b-unsupported-features"></a>B. Recursos sem suporte

Os recursos não compatíveis com certos cenários de OLTP in-memory são descritos em:

- [Recursos do SQL Server sem suporte para OLTP na Memória](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)


As subseções a seguir destacam alguns dos mais importantes recursos sem suporte.


### <a name="b1-snapshot-of-a-database"></a>B.1 INSTANTÂNEO de um banco de dados

Após a primeira vez em que qualquer tabela ou módulo com otimização de memória é criado em um banco de dados, nenhum [INSTANTÂNEO](../../relational-databases/databases/database-snapshots-sql-server.md) do banco de dados pode ser feito. O motivo específico é que:

- o primeiro item com otimização de memória torna impossível remover o último arquivo do GRUPO DE ARQUIVOS com otimização de memória; e
- Nenhum banco de dados que tenha um arquivo em um GRUPO DE ARQUIVOS com otimização de memória pode dar suporte a um INSTANTÂNEO.

Normalmente, um INSTANTÂNEO pode ser útil para iterações de testes rápidas.


### <a name="b2-cross-database-queries"></a>B.2 Consultas entre bancos de dados

Tabelas com otimização de memória não dão suporte a transações [entre bancos de dados](../../relational-databases/in-memory-oltp/cross-database-queries.md) . Você não pode acessar outro banco de dados da mesma transação ou na mesma consulta que também acesse uma tabela com otimização de memória.

Variáveis de tabela não são transacionais. Portanto, [variáveis de tabela com otimização de memória](../../relational-databases/in-memory-oltp/faster-temp-table-and-table-variable-by-using-memory-optimization.md) podem ser usadas em consultas entre bancos de dados.


### <a name="b3-readpast-table-hint"></a>B.3 Dica de tabela READPAST

Nenhuma consulta pode aplicar a [dica de tabela](../../t-sql/queries/hints-transact-sql-table.md) READPAST a qualquer tabela com otimização de memória.

A dica READPAST é útil em cenários em que várias sessões estão acessando e modificando o mesmo conjunto pequeno de linhas, como ao processar uma fila.


### <a name="b4-rowversion-sequence"></a>B.4 RowVersion, sequência

- Nenhuma coluna pode ser marcada para [RowVersion](../../t-sql/data-types/rowversion-transact-sql.md) em uma tabela com otimização de memória.


- Não é possível usar [SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md) com uma restrição em uma tabela com otimização de memória. Por exemplo, não é possível criar uma restrição DEFAULT com uma cláusula NEXT VALUE FOR. SEQUENCEs podem ser usados com instruções INSERT e UPDATE.


## <a name="c-administrative-maintenance"></a>C. Manutenção administrativa


Esta seção descreve diferenças na administração de bancos de dados em que tabelas com otimização de memória são usadas.


### <a name="c1-identity-seed-reset-increment--1"></a>C. 1 Redefinição de semente de identidade, incremento > 1

[DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md), para propagar uma coluna IDENTITY, não pode ser usado em uma tabela com otimização de memória.

O valor do incremento é restrito a exatamente 1 para uma coluna IDENTITY em uma tabela com otimização de memória.


### <a name="c2-dbcc-checkdb-cannot-validate-memory-optimized-tables"></a>C. 2 DBCC CHECKDB não pode validar tabelas com otimização de memória

O comando [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) não faz nada quando o destino é uma tabela com otimização de memória. As seguintes etapas são uma solução alternativa:


1. [Fazer backup do log de transações](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md).

2. Faça backup dos arquivos no GRUPO DE ARQUIVOS com otimização de memória para um dispositivo nulo. O processo de backup invoca uma validação de soma de verificação.

    Se forem encontrados danos, continue com as próximas etapas.

3. Copie os dados das tabelas com otimização de memória para tabelas baseadas em disco, para armazenamento temporário.

4. Restaure os arquivos do GRUPO DE ARQUIVOS com otimização de memória.

5. INSIRA nas tabelas com otimização de memória os dados armazenados temporariamente nas tabelas baseadas em disco.

6. DESCARTE as tabelas baseadas em disco que mantinham os dados temporariamente.



## <a name="d-performance"></a>D. Desempenho

Esta seção descreve situações em que o desempenho excelente de tabelas com otimização de memória pode ficar abaixo de seu potencial completo.


### <a name="d1-index-considerations"></a>D.1 Considerações sobre índices

Todos os índices em uma tabela com otimização de memória são criados e gerenciados pelas instruções CREATE TABLE e ALTER TABLE relacionadas à tabela. Você não pode ter uma tabela com otimização de memória como alvo de uma instrução CREATE INDEX.

O índice não clusterizado de árvore B tradicional normalmente é a opção mais sensata e simples quando você implementa pela primeira vez uma tabela com otimização de memória. Posteriormente, depois de ver o desempenho do seu aplicativo, você pode considerar passar para outro tipo de índice.

Dois tipos especiais de índices precisam de discussão no contexto de uma tabela com otimização de memória: índices columnstore e índices de hash.

Para ter uma visão geral dos índices em tabelas com otimização de memória, consulte:

- [Índices para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)


#### <a name="hash-indexes"></a>Índices de hash

Índices de hash podem ser a forma mais rápida de acessar uma linha específica pelo valor exato de sua chave primária usando o operador " **=** ".

- Operadores inexatos como ‘ **! =** ’, ‘ **>** ’ ou ‘**BETWEEN**’ prejudicariam o desempenho se usados com um índice de hash.

- Um índice de hash poderá não ser a melhor opção se a taxa de duplicação do valor da chave se tornar muito alta.

- Evite subestimar a quantidade de *buckets* de que seu índice de hash pode precisar para evitar longas cadeias dentro de buckets individuais. Para obter detalhes, confira:
    - [Índices de hash para tabelas com otimização de memória](../../relational-databases/in-memory-oltp/hash-indexes-for-memory-optimized-tables.md)


#### <a name="nonclustered-columnstore-indexes"></a>Índices columnstore não clusterizados

Tabelas com otimização de memória oferecem alta taxa de transferência de dados de transações comerciais típicos, no paradigma que chamamos de *transação online* ou *OLTP*. Índices de columnStore oferecem alta taxa de transferência de agregações e processamentos semelhantes que chamamos de *Análise*. No passado, a melhor abordagem disponível para atender às necessidades de OLTP e Análise era ter tabelas separadas com grande movimentação de dados e com algum grau de duplicação de dados. Hoje, uma **solução híbrida** mais simples está disponível: ter um índice de columnstore em uma tabela com otimização de memória.


- Um [índice de columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md) pode ser interno a uma tabela baseada em disco, até mesmo como o índice clusterizado. Mas, em uma tabela com otimização de memória, um índice de columnstore não pode ser clusterizado.


- Colunas de LOB ou fora da linha para uma tabela com otimização de memória impedem a criação de um índice de columnstore na tabela.


- Nenhuma instrução ALTER TABLE pode ser executada em uma tabela com otimização de memória enquanto um índice de columnstore existir na tabela.
    - A partir de agosto de 2016, a Microsoft tem planos de curto prazo para melhorar o desempenho da recriação do índice de columnstore.



### <a name="d2-lob-and-off-row-columns"></a>D.2 Colunas de LOB e fora de linha

Objetos grandes (LOBs) são colunas como varchar (**max**). Ter duas colunas de LOB em uma tabela com otimização de memória provavelmente não causa danos suficientes no desempenho para ter importância. Mas evite ter mais colunas de LOB do que seus dados precisam. O mesmo conselho se aplica a colunas fora de linha. Não defina uma coluna como nvarchar(3072) se varchar(512) for suficiente.


Um pouco mais sobre colunas de LOB e fora de linha está disponível em:

- [Tamanho da tabela e da linha em tabelas com otimização de memória](../../relational-databases/in-memory-oltp/table-and-row-size-in-memory-optimized-tables.md)
- [Tipos de Dados com Suporte para o OLTP na Memória](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)



## <a name="e-limitations-of-native-procs"></a>E. Limitações dos procedimentos nativos


Não há suporte para elementos específicos do Transact-SQL em módulos T-SQL compilados nativamente, incluindo procedimentos armazenados. Para obter detalhes sobre quais recursos têm suporte, consulte:

- [Recursos com suporte para módulos T-SQL compilados nativamente](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)

Para obter considerações ao migrar um módulo Transact-SQL que usa recursos sem suporte para procedimentos compilados nativamente, consulte:

- [Problemas de migração para procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/migration-issues-for-natively-compiled-stored-procedures.md)

Além das limitações em determinados elementos do Transact-SQL, também há limitação de operadores de consulta com suporte em módulos T-SQL compilados nativamente. Devido a essas limitações, os procedimentos armazenados compilados nativamente não são adequados para consultas analíticas que processam grandes conjuntos de dados.

#### <a name="no-parallel-processing-in-a-native-proc"></a>Não há processamento paralelo em um procedimento nativo

O processamento paralelo não pode fazer parte de nenhum plano de consulta para um procedimento nativo. Procedimentos nativos são sempre do tipo single-threaded.


#### <a name="join-types"></a>Tipos de junção


Nem uma junção de hash nem uma junção de mesclagem podem fazer parte de qualquer plano de consulta para um procedimento nativo. Junções de loops aninhados são usadas.


#### <a name="no-hash-aggregation"></a>Não há agregação de hash

Quando o plano de consulta para um processo nativo requer uma fase de agregação, somente a agregação de fluxo está disponível. Não há suporte para agregação de hash em um plano de consulta para um procedimento nativo.

- A agregação de hash é melhor quando dados de um grande número de linhas precisam ser agregados.



## <a name="f-application-design-transactions-and-retry-logic"></a>F. Design de aplicativos: transações e lógica de repetição

Uma transação que envolve uma tabela com otimização de memória pode se tornar dependente de outra transação que envolve a mesma tabela. Se a contagem de transações dependentes ultrapassar o máximo permitido, todas as transações dependentes falharão.

No o SQL Server 2016:

- O máximo permitido é de 8 transações dependentes. 8 também é o limite de transações de que qualquer transação pode ser dependente.
- O número do erro é 41839. (No SQL Server 2014, o número do erro é 41301.)


Você pode tornar seus scripts do Transact-SQL mais robustos contra possíveis erros de transação adicionando a *lógica de repetição* a eles. A lógica de repetição tem mais chances de ajudar quando as chamadas UPDATE e DELETE são frequentes ou se a tabela com otimização de memória for referenciada por uma chave estrangeira em outra tabela. Para obter detalhes, confira:

- [Transações com tabelas com otimização de memória](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)
- [Limites de dependência de transações em tabelas otimizadas para memória – Erro 41839](https://blogs.msdn.microsoft.com/sqlcat/2016/07/11/transaction-dependency-limits-with-memory-optimized-tables-error-41839/)



## <a name="related-links"></a>Links relacionados

- [OLTP na memória (otimização na memória)](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)


