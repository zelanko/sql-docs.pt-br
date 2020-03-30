---
title: Tabelas temporais | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: e442303d-4de1-494e-94e4-4f66c29b5fb9
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 60026dd35a22ccf5ea693619912ef1aadab77745
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74165703"
---
# <a name="temporal-tables"></a>Tabelas temporais

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

O SQL Server 2016 introduziu o suporte para tabelas temporais (também conhecidas como tabelas temporais com versão do sistema) como um recurso de banco de dados que oferece suporte interno para fornecer informações sobre os dados armazenados na tabela em qualquer ponto no tempo, em vez de apenas os dados que estão corretos atualmente. Temporal é um recurso de banco de dados que foi introduzido no ANSI SQL 2011.

**Início rápido**

- **Introdução:**

  - [Introdução a tabelas temporais com controle da versão do sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
  - [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
  - [Cenários de uso da tabela temporal](../../relational-databases/tables/temporal-table-usage-scenarios.md)

  - [Introdução às tabelas temporais no Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-temporal-tables/)

- **Exemplos:**

  - [Criando uma tabela temporal com controle de versão do sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
  - [Trabalhando com tabelas temporais com controle da versão do sistema e otimização de memória](../../relational-databases/tables/working-with-memory-optimized-system-versioned-temporal-tables.md)
  - [Modificando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
  - [Consultando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
  - **Baixar o banco de dados de exemplo do Adventure Works:** Para começar a usar Tabelas Temporais, baixe o [banco de dados AdventureWorks para SQL Server 2016 CTP3](https://www.microsoft.com/download/details.aspx?id=49502) com exemplos de script e siga as instruções na pasta 'Temporal'

- **Sintaxe:**

  - [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)
  - [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
  - [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)
- **Vídeo:** Para obter uma discussão de 20 minutos sobre o recurso temporal, veja [Temporal no SQL Server 2016](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).

## <a name="what-is-a-system-versioned-temporal-table"></a>O que é uma tabela temporal com versão do sistema

Uma tabela temporal com versão do sistema é um tipo de tabela de usuário criada para manter um histórico completo de alterações de dados e permitir uma análise fácil de pontos no tempo. Esse tipo de tabela temporal é conhecido como tabela temporal com versão do sistema porque o período de validade para cada linha é gerenciado pelo sistema (ou seja, o mecanismo de banco de dados).

Cada tabela temporal tem duas colunas explicitamente definidas, cada um com um tipo de dados **datetime2** . Essas colunas são chamadas de colunas de período. Essas colunas de período são usadas exclusivamente pelo sistema para gravar o período de validade para cada linha sempre que uma linha é modificada.

Além dessas colunas de período, uma tabela temporal também contém uma referência a outra tabela com um esquema espelhado. O sistema usa essa tabela para armazenar a versão anterior da linha automaticamente sempre que uma linha na tabela temporal é atualizada ou excluída. Essa tabela adicional é conhecida como a tabela de histórico, enquanto a tabela principal que armazena as versões atuais (reais) das linhas é conhecida como a tabela atual ou simplesmente como a tabela temporal. Durante a criação da tabela temporal, os usuários podem especificar uma tabela de histórico existente (deve ter um esquema compatível) ou deixar que o sistema crie a tabela de histórico padrão.

## <a name="why-temporal"></a>Por que temporal

As fontes de dados reais são dinâmicas e geralmente as decisões comerciais dependem das informações que os analistas podem obter da evolução dos dados. Os casos de uso de tabelas temporais incluem:

- Auditar todas as alterações de dados e executar análise forense de dados quando necessário
- Reconstruir o estado dos dados a partir de qualquer momento no passado
- Calcular tendências ao longo do tempo
- Manter uma dimensão de alteração lenta para aplicações de suporte a decisões
- Recuperar alterações acidentais em dados e erros de aplicativos

## <a name="how-does-temporal-work"></a>Como funciona a tabela temporal

 A versão do sistema para uma tabela é implementada como um par de tabelas, uma tabela atual e uma tabela de histórico. Dentro de cada uma dessas tabelas, as seguintes colunas **datetime2** adicionais são usadas para definir o período de validade para cada registro:

- Coluna de início do período: O sistema registra a hora de início da linha na coluna, normalmente denotada como a coluna **SysStartTime**.
- Coluna de término do período: O sistema registra a hora de término da linha na coluna, normalmente indicada como a coluna **SysEndTime**.

A tabela atual contém o valor atual para cada linha. A tabela de histórico contém cada valor anterior para cada linha, se houver, e a hora de início e término do período para o qual ela era válida.

![Temporal-HowWorks](../../relational-databases/tables/media/temporal-howworks.PNG "Temporal-HowWorks")

O exemplo simples a seguir ilustra um cenário com informações de Funcionário em um banco de dados de RH hipotético:

```sql
CREATE TABLE dbo.Employee
(
  [EmployeeID] int NOT NULL PRIMARY KEY CLUSTERED
  , [Name] nvarchar(100) NOT NULL
  , [Position] varchar(100) NOT NULL
  , [Department] varchar(100) NOT NULL
  , [Address] nvarchar(1024) NOT NULL
  , [AnnualSalary] decimal (10,2) NOT NULL
  , [ValidFrom] datetime2 GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )
WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.EmployeeHistory));
```

- **INSERTS:** Em uma **INSERT**, o sistema define o valor para a coluna **SysStartTime** como a hora de início da transação atual (no fuso horário UTC) com base no relógio do sistema e atribui o valor para a coluna **SysEndTime** para o valor máximo de 9999-12-31. Isso marca a linha como aberta.
- **UPDATES:** Em uma **UPDATE**, o sistema armazena o valor anterior do registro na tabela de histórico e define o valor para a coluna **SysEndTime** como a hora de início da transação atual (no fuso horário UTC) com base no relógio do sistema. Isso marca a linha como fechada, com um período registrado para o qual a linha era válida. Na tabela atual, o registro é atualizado com o novo valor e o sistema define o valor para a coluna **SysStartTime** para a hora de início da transação (no fuso horário UTC) com base no relógio do sistema. O valor de registro atualizado na tabela atual para a coluna **SysEndTime** permanece o valor máximo de 9999-12-31.
- **DELETES:** Em uma **DELETE**, o sistema armazena o valor anterior do registro na tabela de histórico e define o valor para a coluna **SysEndTime** como a hora de início da transação atual (no fuso horário UTC) com base no relógio do sistema. Isso marca a linha como fechada, com um período registrado para o qual a linha anterior era válida. Na tabela atual, a linha é removida. As consultas da tabela atual não retornarão essa linha. Somente as consultas que lidam com dados de histórico retornarão dados cujo linha está fechada.
- **MERGE:** Em uma **MERGE**, a operação se comporta exatamente como se até três instruções (uma **INSERT**, uma **UPDATE** e/ou uma **DELETE**) fossem executadas, dependendo do que é especificado como ações na instrução **MERGE**.

> [!IMPORTANT]
> As horas registradas nas colunas datetime2 do sistema baseiam-se na hora de início da própria transação. Por exemplo, todas as linhas inseridas em uma única transação terão o mesmo horário UTC registrado na coluna correspondente ao início do período **SYSTEM_TIME** .

## <a name="how-do-i-query-temporal-data"></a>Como faço para consultar dados temporais

A cláusula **FROM** _\<table\>_ da instrução **SELECT** tem uma nova cláusula **FOR SYSTEM_TIME** com cinco subcláusulas temporais específicas para consultar dados das tabelas atual e histórica. Essa nova sintaxe de instrução **SELECT** é suportada diretamente em uma única tabela, propagada por meio de várias associações e exibições em várias tabelas temporais.

![Temporal-Querying](../../relational-databases/tables/media/temporal-querying.PNG "Temporal-Querying")

A consulta a seguir procura por versões de linha da linha Employee com EmployeeID = 1000 que estavam ativas durante, pelo menos, parte do período entre 1º de janeiro de 2014 e 1º de janeiro de 2015 (incluindo o limite superior):

```sql
SELECT * FROM Employee
  FOR SYSTEM_TIME
    BETWEEN '2014-01-01 00:00:00.0000000' AND '2015-01-01 00:00:00.0000000'
      WHERE EmployeeID = 1000 ORDER BY ValidFrom;
```

> [!NOTE]
> **FOR SYSTEM_TIME** filtra as linhas que têm um período de validade com duração zero (**SysStartTime** = **SysEndTime**).
> Essas linhas serão geradas se você realizar várias atualizações na mesma chave primária na mesma transação.
> Nesse caso, a consulta temporal exibe somente versões de linha anteriores às transações e que se tornaram reais após as transações.
> Se você precisa incluir as linhas na análise, veja diretamente a tabela de histórico.

Na tabela a seguir, SysStartTime na coluna Qualifying Rows representa o valor na coluna **SysStartTime** da tabela que está sendo consultada e **SysEndTime** representa o valor da coluna **SysEndTime** da tabela que está sendo consultada. Para obter a sintaxe completa e exemplos, veja [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md) e [Consultando dados em uma tabela temporal com controle da versão do sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md).

|Expression|Linhas de qualificação|Descrição|
|----------------|---------------------|-----------------|
|**AS OF**<date_time>|SysStartTime \<= date_time AND SysEndTime > date_time|Retorna uma tabela com uma linha que contém os valores que foram reais (atuais) no momento especificado no passado. Internamente, uma união é executada entre a tabela temporal e sua tabela de histórico e os resultados são filtrados para retornar os valores na linha que era válida no ponto no tempo especificado pelo parâmetro *<date_time>* . O valor de uma linha é considerado válido se o valor de *system_start_time_column_name* é menor ou igual ao valor do parâmetro *<date_time>* e o valor de *system_end_time_column_name* é maior que o valor do parâmetro *<date_time>* .|
|**FROM**<start_date_time>**TO**<end_date_time>|SysStartTime < end_date_time AND SysEndTime > start_date_time|Retorna uma tabela com os valores para todas as versões de linha que estavam ativas no intervalo de tempo especificado, não importando se eles começaram a ser ativos antes do valor de parâmetro *<start_date_time>* para o argumento FROM ou deixaram de ser ativos após o valor de parâmetro *<end_date_time>* para o argumento TO. Internamente, uma união é executada entre a tabela temporal e sua tabela de histórico e os resultados são filtrados para retornar os valores para todas as versões de linha que estavam ativas a qualquer momento durante o intervalo de tempo especificado. As linhas que deixaram de ser ativas exatamente no limite inferior definido pelo ponto de extremidade FROM não são incluídas e os registros que se tornaram ativos exatamente no limite superior definido pelo ponto de extremidade TO também não são incluídos.|
|**BETWEEN**<start_date_time>**AND**<end_date_time>|SysStartTime \<= end_date_time AND SysEndTime > start_date_time|A mesma descrição acima para **FOR SYSTEM_TIME FROM** <start_date_time>**TO** <end_date_time> é válida, exceto que a tabela de linhas retornada inclui linhas que se tornaram ativas no limite superior definido pelo ponto de extremidade <end_date_time>.|
|**CONTAINED IN** (<start_date_time> , <end_date_time>)|SysStartTime >= start_date_time AND SysEndTime \<= end_date_time|Retorna uma tabela com os valores para todas as versões de linha que foram abertas e fechadas dentro do intervalo de tempo especificado definido por dois valores de data e hora para o argumento CONTAINED IN. As linhas que se tornaram ativas exatamente no limite inferior ou que deixaram de ser ativas exatamente no limite superior são incluídas.|
|**ALL**|Todas as linhas|Retorna a união de linhas que pertencem às tabelas atual e de histórico.|

> [!NOTE]
> Opcionalmente, é possível optar por ocultar essas colunas de período, de modo que as consultas que referenciam explicitamente essas colunas não as retornarão (o cenário **SELECT \* FROM** _\<table\>_ ). Para retornar uma coluna oculta, basta fazer referência explícita à coluna oculta na consulta. Da mesma forma, as instruções **INSERT** e **BULK INSERT** continuarão como se as novas colunas de período não estivessem presentes (e os valores da coluna serão populados automaticamente). Para obter detalhes sobre como usar a cláusula **HIDDEN** , veja [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) e [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md).

## <a name="next-steps"></a>Próximas etapas

- [Introdução a tabelas temporais com controle da versão do sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [Cenários de uso da tabela temporal](../../relational-databases/tables/temporal-table-usage-scenarios.md)
- [Considerações e limitações da tabela temporal](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Particionamento com tabelas temporais](../../relational-databases/tables/partitioning-with-temporal-tables.md)
- [Verificações de consistência do sistema de tabela temporal](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [Segurança da tabela temporal](../../relational-databases/tables/temporal-table-security.md)
- [Funções e exibições de metadados de tabela temporal](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
