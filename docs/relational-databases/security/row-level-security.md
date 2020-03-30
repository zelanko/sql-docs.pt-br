---
title: Segurança em nível de linha | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- access control predicates
- row level security
- security [SQL Server], predicate based access control
- row level security described
- predicate based security
ms.assetid: 7221fa4e-ca4a-4d5c-9f93-1b8a4af7b9e8
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f9e604ba803b1116c9867071f547a1d1958437b7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "78288972"
---
# <a name="row-level-security"></a>Segurança em nível de linha

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  ![Gráfico de Segurança em Nível de Linha](../../relational-databases/security/media/row-level-security-graphic.png "Gráfico de Segurança em Nível de Linha")  
  
A Segurança em nível de linha permite que você use o contexto de execução ou a associação de grupo para controlar o acesso às linhas em uma tabela de banco de dados.
  
O RLS (nível de linha de segurança) simplifica o design e a codificação de segurança em seu aplicativo. O RLS ajuda a implementar restrições de acesso a linhas de dados. Por exemplo, você pode garantir que os funcionários acessem somente as linhas de dados que são relevantes aos seus departamentos. Outro exemplo é restringir o acesso a dados dos clientes apenas aos dados relevantes para sua empresa.  
  
A lógica de restrição de acesso é localizado na camada de banco de dados, em vez de longe dos dados em outra camada de aplicativo. O sistema de banco de dados aplica as restrições de acesso toda vez que há tentativa de acesso a dados a partir de qualquer camada. Isso torna o sistema de segurança mais robusto e confiável, reduzindo a área de superfície do sistema de segurança.  
  
Implemente a RLS usando a instrução [CREATE SECURITY POLICY](../../t-sql/statements/create-security-policy-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] e predicados criados como [funções com valor de tabela embutida](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md).  

**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Obter](https://azure.microsoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)), [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].
  
> [!NOTE]
> O SQL Data Warehouse do Azure só dá suporte para predicados de filtro. Os predicados de bloqueio não têm suporte no SQL Data Warehouse do Azure no momento.

## <a name="description"></a><a name="Description"></a> Descrição

A RLS permite dois tipos de predicado de segurança.  
  
- Os predicados de filtro filtram silenciosamente as linhas disponíveis para operações de leitura (SELECT, UPDATE e DELETE).  
  
- Os predicados de bloqueio bloqueiam explicitamente as operações de gravação (AFTER INSERT, AFTER UPDATE, BEFORE UPDATE, BEFORE DELETE) que violam o predicado.  
  
 O acesso aos dados no nível de linha em uma tabela é restrito por um predicado de segurança definido como uma função com valor de tabela embutida. A função é então invocada e imposta por uma política de segurança. Para predicados de filtro, não há nenhuma indicação ao aplicativo de que as linhas tenham sido filtradas no conjunto de resultados. Se todas as linhas forem filtradas, um conjunto de null será retornado. Para predicados de bloqueio, todas as operações que violem o predicado falharão com um erro.  
  
 Predicados de filtro são aplicados durante a leitura de dados da tabela base. Eles afetam todas as operações get: **SELECT**, **DELETE** e **UPDATE**. Os usuários não podem selecionar ou excluir linhas que são filtradas. Os usuários não podem atualizar as linhas que são filtradas. Mas, é possível atualizar linhas de forma que elas sejam filtradas posteriormente. Os predicados de bloqueio afetam todas as operações de gravação.  
  
- Os predicados AFTER INSERT e AFTER UPDATE podem impedir que os usuários atualizem linhas para valores que violem o predicado.  
  
- Os predicados BEFORE UPDATE podem impedir que os usuários atualizem linhas que atualmente violem o predicado.  
  
- Os predicados BEFORE DELETE podem bloquear operações de exclusão.  
  
 Os predicados de filtro e bloqueio, bem como as políticas de segurança têm o seguinte comportamento:  
  
- Você pode definir uma função de predicado que se une a outra tabela e/ou invoca uma função. Se a política de segurança for criada com `SCHEMABINDING = ON` (o padrão), a junção ou função será acessível pela consulta e funcionará como o esperado, sem nenhuma verificação de permissão adicional. Se a política de segurança for criada com `SCHEMABINDING = OFF`, os usuários precisarão ter permissões **SELECT** nessas tabelas e funções adicionais para consultar a tabela de destino. Se a função de predicado invocar uma função de valor escalar CLR, a permissão **EXECUTE** também será necessária.
  
- Você pode fazer uma consulta em uma tabela que tenha um predicado de segurança definido mas desabilitado. Quaisquer linhas que tenham sido filtradas ou bloqueadas não serão afetadas.  
  
- Se um usuário dbo, um membro da função **db_owner** ou o proprietário da tabela fizer uma consulta em uma tabela que tem uma política de segurança definida e habilitada, as linhas serão filtradas ou bloqueadas conforme definido pela política de segurança.  
  
- As tentativas de alterar o esquema de uma tabela associada por uma política de segurança associada ao esquema resultarão em um erro. No entanto, as colunas não referenciadas pelo predicado podem ser alteradas.  
  
- Tentar adicionar um predicado em uma tabela que já tenha um definido para a operação especificada resultará em um erro. Isso ocorrerá se o predicado estiver habilitado ou não.
  
- As tentativas de modificar uma função que é usada como um predicado em uma tabela em uma política de segurança associada ao esquema resultarão em um erro.  
  
- Definir múltiplas políticas de segurança ativas que contêm predicados não sobrepostos é uma ação que terá êxito.  
  
 Os predicados de filtro apresentam o seguinte comportamento:  
  
- Defina uma política de segurança que filtra as linhas de uma tabela. O aplicativo não tem conhecimento de nenhuma linha filtrada nas operações **SELECT**, **UPDATE** e **DELETE**. Incluindo situações em que todas as linhas são filtradas. O aplicativo pode fazer **INSERT** de linhas, mesmo que elas sejam filtradas durante qualquer outra operação.  
  
 Os predicados de bloqueio apresentam o seguinte comportamento:  
  
- Os predicados de bloqueio para UPDATE são divididos em operações distintas para BEFORE e AFTER. Consequentemente, não é possível, por exemplo, impedir os usuários de atualizar uma linha para ter um valor maior que o atual. Se esse tipo de lógica for necessário, você deverá usar gatilhos com as tabelas intermediárias [DELETED e INSERTED](../triggers/use-the-inserted-and-deleted-tables.md) para fazer referência a valores novos e antigos juntos.  
  
- O otimizador não verificará um predicado de bloqueio AFTER UPDATE se as colunas usadas pela função de predicado não forem alteradas. Por exemplo:  Alice não deve conseguir alterar um salário para ser maior que 100.000. Alice pode alterar o endereço de um funcionário cujo salário já seja superior a 100.000, desde que as colunas referenciadas no predicado não tenham sido alteradas.  
  
- Nenhuma mudança foi feita nas APIs em massa, incluindo BULK INSERT. Isso significa que os predicados de bloqueio AFTER INSERT serão aplicados às operações de inserção em massa, assim como seriam em operações de inserção regular.  
  
## <a name="use-cases"></a><a name="UseCases"></a> Casos de uso

 Estes são exemplos de design de como RLS pode ser usado:  
  
- Um hospital pode criar uma diretiva de segurança que permite a enfermeiras exibir linhas de dados somente para seus pacientes.  
  
- Um banco pode criar uma política para restringir o acesso às linhas de dados financeiros com base no cargo ou divisão de negócios de um funcionário na empresa.  
  
- Um aplicativo multilocatário pode criar uma política para impor uma separação lógica entre as linhas de dados de cada locatário e as linhas referentes a todos os outros locatários. Eficiência é obtida pelo armazenamento de dados para vários locatários em uma única tabela. Cada locatário pode ver somente as linhas com seus próprios dados.  
  
 Os predicados de filtro RLS são funcionalmente equivalentes a acrescentar uma cláusula **WHERE** . O predicado pode ser tão sofisticado como ditam as práticas comerciais, ou a cláusula pode ser tão simples quanto `WHERE TenantId = 42`.  
  
 Em termos mais formais, o RLS introduz o controle de acesso baseado em predicado. Ele apresenta uma avaliação centralizada, flexível e baseada em predicado. O predicado pode ser baseado em metadados ou em qualquer outro critério que o administrador determine, como apropriado. O predicado é usado como critério para determinar se o usuário tem acesso apropriado aos dados com base nos atributos de usuário. O controle de acesso baseado em rótulo pode ser implementado usando o controle de acesso baseado em predicado.  
  
## <a name="permissions"></a><a name="Permissions"></a> Permissões

 Criando, alterando ou removendo políticas de segurança requer a permissão **ALTER ANY SECURITY POLICY** . Criar ou descartar uma política de segurança requer a permissão **ALTER** no esquema.  
  
 Além disso, as seguintes permissões são necessárias para cada predicado que é adicionado:  
  
- Permissões**SELECT** e **REFERENCES** na função que está sendo usada como um predicado.  
  
- Permissão**REFERENCES** na tabela de destino que está sendo associada à política.  
  
- permissão**REFERENCES** em todas as colunas da tabela de destino usadas como argumentos.  
  
 Diretivas de segurança se aplicam a todos os usuários, incluindo usuários de dbo do banco de dados. Os usuários do dbo podem alterar ou descartar as políticas de segurança, mas suas alterações às políticas de segurança podem ser auditadas. Se os usuários com altos privilégios, como sysadmin ou db_owner precisarem ver todas as linhas para solucionar problemas ou validar dados, a política de segurança deverá ser escrita para permitir isso.  
  
 Se uma política de segurança for criada com `SCHEMABINDING = OFF`, para consultar a tabela de destino, os usuários deverão ter a permissão  **SELECT** ou **EXECUTE** na função de predicado e em todas as tabelas, exibições ou funções usadas adicionais na função de predicado. Se uma política de segurança for criada com `SCHEMABINDING = ON` (o padrão), essas verificações de permissão serão ignoradas quando os usuários consultarem a tabela de destino.  
  
## <a name="best-practices"></a><a name="Best"></a> Práticas recomendadas  
  
- É altamente recomendável criar um esquema separado para os objetos RLS: funções de predicado e políticas de segurança. Isso ajuda a separar as permissões que são exigidas por esses objetos especiais das tabelas de destino. Uma separação adicional de políticas e funções de predicado diferentes pode ser necessária em bancos de dados multilocatário, mas não como padrão para todos os casos.
  
- A permissão **ALTER ANY SECURITY POLICY** é destinada a usuários altamente privilegiados (como um gerente de políticas de segurança). O gerenciador de políticas de segurança não exige a permissão **SELECT** nas tabelas que protege.  
  
- Evite conversões de tipo em funções de predicado para evitar possíveis erros de runtime.  
  
- Evite a recursão no predicado funções sempre que possível para evitar a degradação do desempenho. O otimizador de consulta tentará detectar as recursões diretas, mas não é garantido que encontrará as recursões indiretas. A recursão indireta é onde uma segunda função chama a função de predicado.  
  
- Evite usar junções de tabelas em excesso em funções de predicado, para maximizar o desempenho.  
  
 Evite a lógica de predicado que dependa de [opções SET](../../t-sql/statements/set-statements-transact-sql.md) específicas da sessão: Embora seja improvável que elas sejam usadas em aplicações práticas, as funções de predicado cuja lógica depende de determinadas opções **SET** específicas da sessão podem perder informações se os usuários conseguem executar consultas arbitrárias. Por exemplo, uma função de predicado que implicitamente converte uma cadeia de caracteres em **datetime** poderia filtrar linhas diferentes com base na opção **SET DATEFORMAT** da sessão atual. Em geral, as funções de predicado devem obedecer as regras a seguir:  
  
- As funções de predicado não devem converter implicitamente cadeias de caracteres em **date**, **smalldatetime**, **datetime**, **datetime2** ou **datetimeoffset**, ou vice-versa, pois essas conversões são afetadas pleas opções [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md) e [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md). Em vez disso, use a função **CONVERT** e especifique explicitamente o parâmetro de estilo.  
  
- As funções de predicado não devem se basear no valor do primeiro dia da semana, pois esse valor é afetado pela opção [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).  
  
- As funções de predicado não devem se basear em expressões aritméticas ou de agregação que retornam **NULL** se forem erro (como um estouro ou divisão por zero) porque esse comportamento é afetado pelas opções [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md), [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md) e [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md).  
  
- As funções de predicado não devem comparar cadeias de caracteres concatenadas com **NULL**, pois esse comportamento é afetado pela opção [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  

## <a name="security-note-side-channel-attacks"></a><a name="SecNote"></a> Observação de segurança: Ataques de canal lateral

### <a name="malicious-security-policy-manager"></a>Gerente de política de segurança mal-intencionado

É importante observar que um gerente de política de segurança mal-intencionado, com permissões suficientes para criar uma política de segurança na parte superior de uma coluna confidencial, tendo permissão para criar ou alterar funções embutidas com valor de tabela, poderá conspirar com outro usuário que tenha permissões SELECT em uma tabela para realizar a exportação de dados, pela criação mal-intencionada de funções embutidas com valor de tabela, projetadas para usar ataques de temporização para inferir dados. Esses ataques exigiriam a colusão (ou excesso de permissões concedidas a um usuário mal-intencionado) e provavelmente demandariam várias iterações de modificação da política (exigindo permissão para remover o predicado, para que pudessem então quebrar a associação do esquema), modificando as funções com valor de tabela embutida e repetidamente executando instruções de seleção na tabela de destino. É recomendável limitar as permissões conforme necessário e o monitor para qualquer atividade suspeita. As atividade como políticas em constante mudança e as funções com valor de tabela em linha relacionadas à segurança em nível de linha devem ser monitoradas.  
  
### <a name="carefully-crafted-queries"></a>Consultas cuidadosamente elaboradas

É possível causar vazamento de informações pelo uso de consultas concebidas cuidadosamente. Por exemplo, `SELECT 1/(SALARY-100000) FROM PAYROLL WHERE NAME='John Doe'` permitiria que um usuário mal-intencionado soubesse que o salário de John Doe é US$ 100.000. Mesmo que haja um predicado de segurança em vigor para impedir que um usuário mal-intencionado consulte diretamente o salário de outras pessoas, o usuário pode determinar quando a consulta retorna uma exceção de divisão por zero.  

## <a name="cross-feature-compatibility"></a><a name="Limitations"></a> Compatibilidade entre recursos

 De modo geral, a segurança no nível de linha funcionará conforme o esperado entre os recursos. No entanto, há algumas exceções. Esta seção documenta várias observações e limitações para o uso da segurança em nível de linha com determinados recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
- **DBCC SHOW_STATISTICS** relata estatísticas de dados não filtrados e pode perder informações que, de outra forma, estariam protegidas por uma política de segurança. Por esse motivo, o acesso para exibir um objeto de estatísticas para uma tabela com uma política de segurança de nível de linha é restrito. O usuário deve possuir a tabela ou ser um membro da função de servidor fixa sysadmin, da função de banco de dados fixa db_owner ou da função de banco de dados fixa db_ddladmin.  
  
- **Filestream:** a RLS não é compatível com Filestream.  
  
- **PolyBase:** a RLS é compatível com tabelas externas do Polybase somente no SQL Data Warehouse do Azure.

- **Tabelas com otimização de memória:** a função com valor de tabela embutida usada como um predicado de segurança em uma tabela com otimização de memória deve ser definida usando a opção `WITH NATIVE_COMPILATION`. Com essa opção, os recursos de linguagem não permitidos pelas tabelas com otimização de memória serão banidos e o erro apropriado será emitido no momento da criação. Para obter mais informações, veja a seção **Segurança em nível de linha em tabelas com otimização de memória** em [Introdução às tabelas com otimização de memória](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md).  
  
- **Exibições indexadas:** de modo geral, as políticas de segurança podem ser criadas sobre as exibições, e as exibições podem ser criadas sobre as tabelas que são associadas pelas políticas de segurança. No entanto, as exibições indexadas não podem ser criadas sobre as tabelas que têm uma política de segurança, pois as pesquisas de linha pelo índice contornariam a política.  
  
- **Captura de Dados de Alterações:** a Captura de Dados de Alterações pode perder linhas inteiras que devem ser filtradas para membros do **db_owner** ou para usuários que são membros da função "gating" especificada quando a CDC é habilitada para uma tabela (observação: você pode definir essa função explicitamente para **NULL** a fim de permitir que todos os usuários acessem os dados alterados). Na verdade, **db_owner** e os membros dessa função gating poderão ver todas as alterações nos dados de uma tabela, mesmo se houver uma política de segurança na tabela.  
  
- **Controle de Alterações:** o Controle de Alterações pode deixar vazar a chave primária de linhas que deve ser filtrada para usuários com as permissões **SELECT** e **VIEW CHANGE TRACKING**. Os valores de dados reais não vazam; apenas o fato de que a coluna A foi atualizada/inserida/excluída para a linha com a chave primária B. Isso será um problema se a chave primária contiver um elemento confidencial, como um Número de Seguro Social. No entanto, na prática, esse **CHANGETABLE** é quase sempre unido à tabela original para obtenção de dados mais recentes.  
  
- **Pesquisa de Texto Completo:** um impacto no desempenho é esperado em consultas que usam as funções de Pesquisa de Texto Completo e Pesquisa Semântica, devido a uma junção extra introduzida para aplicar a Segurança em Nível de Linha e evitar a perda das chaves primárias de linhas que devem ser filtradas: **CONTAINSTABLE**, **FREETEXTTABLE**, semantickeyphrasetable, semanticsimilaritydetailstable, semanticsimilaritytable.  
  
- **Índices Columnstore:** a RLS é compatível com índices columnstore clusterizados e não clusterizados. No entanto, como a segurança no nível de linha se aplica a uma função, é possível que o otimizador possa modificar o plano de consulta, de modo que ele não use o modo de lote.  
  
- **Exibições Particionadas:** os predicados de bloqueio não podem ser definidos em exibições particionadas, e as exibições particionadas não podem ser criadas sobre as tabelas que usam predicados de bloqueio. Os predicados de filtro são compatíveis com exibições particionadas.  
  
- **Tabelas Temporais:** as tabelas temporais são compatíveis com a RLS. No entanto, os predicados de segurança na tabela atual não são replicados automaticamente na tabela de histórico. Para aplicar uma política de segurança às tabelas atual e de histórico, você deverá adicionar individualmente um predicado de segurança em cada tabela.  
  
## <a name="examples"></a><a name="CodeExamples"></a> Exemplos  
  
### <a name="a-scenario-for-users-who-authenticate-to-the-database"></a><a name="Typical"></a> A. Cenário para usuários que se autenticam no banco de dados

 Este exemplo cria três usuários e cria e preenche uma tabela com seis linhas. Em seguida, ele cria uma função com valor de tabela embutida e uma política de segurança para a tabela. O exemplo, em seguida, mostra como as instruções select são filtrados para os diversos usuários.  
  
 Crie três contas de usuário que demonstrem os diferentes recursos de acesso.  

> [!NOTE]
> O SQL Data Warehouse do Azure não dá suporte para EXECUTE AS USER. Dessa maneira, é necessário usar CREATE LOGIN para cada usuário com antecedência. Posteriormente, você fará logon como o usuário apropriado para testar esse comportamento.

```sql  
CREATE USER Manager WITHOUT LOGIN;  
CREATE USER Sales1 WITHOUT LOGIN;  
CREATE USER Sales2 WITHOUT LOGIN;  
```

Crie uma tabela para armazenar dados.  

```sql
CREATE TABLE Sales  
    (  
    OrderID int,  
    SalesRep sysname,  
    Product varchar(10),  
    Qty int  
    );  
```

 Preencha a tabela com seis linhas de dados, mostrando três pedidos para cada representante de vendas.  

```sql
INSERT INTO Sales VALUES (1, 'Sales1', 'Valve', 5);
INSERT INTO Sales VALUES (2, 'Sales1', 'Wheel', 2);
INSERT INTO Sales VALUES (3, 'Sales1', 'Valve', 4);
INSERT INTO Sales VALUES (4, 'Sales2', 'Bracket', 2);
INSERT INTO Sales VALUES (5, 'Sales2', 'Wheel', 5);
INSERT INTO Sales VALUES (6, 'Sales2', 'Seat', 5);
-- View the 6 rows in the table  
SELECT * FROM Sales;
```

Conceda acesso de leitura à tabela para cada usuário.  

```sql
GRANT SELECT ON Sales TO Manager;  
GRANT SELECT ON Sales TO Sales1;  
GRANT SELECT ON Sales TO Sales2;  
```

Crie um novo esquema e uma função com valor de tabela embutida. A função retorna 1 quando uma linha da coluna do representante de vendas é o mesmo que o usuário que executa a consulta (`@SalesRep = USER_NAME()`) ou se o usuário executando a consulta for o gerente (`USER_NAME() = 'Manager'`).

```sql
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@SalesRep AS sysname)  
    RETURNS TABLE  
WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result
WHERE @SalesRep = USER_NAME() OR USER_NAME() = 'Manager';  
```

Crie uma política de segurança adicionando a função como um predicado de filtro. O estado deve ser definido como ON para habilitar a política.

```sql
CREATE SECURITY POLICY SalesFilter  
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesRep)
ON dbo.Sales  
WITH (STATE = ON);  
```

Permitir permissões SELECT na função fn_securitypredicate 
```sql
GRANT SELECT ON security.fn_securitypredicate TO Manager;  
GRANT SELECT ON security.fn_securitypredicate TO Sales1;  
GRANT SELECT ON security.fn_securitypredicate TO Sales2;  
```


Agora teste o predicado de filtragem selecionando-o a partir da tabela Vendas como cada usuário.

```sql
EXECUTE AS USER = 'Sales1';  
SELECT * FROM Sales;
REVERT;  
  
EXECUTE AS USER = 'Sales2';  
SELECT * FROM Sales;
REVERT;  
  
EXECUTE AS USER = 'Manager';  
SELECT * FROM Sales;
REVERT;  
```

> [!NOTE]
> O SQL Data Warehouse do Azure não dá suporte para EXECUTE AS USER. Desse modo, faça logon como o usuário apropriado para testar o comportamento acima.

O gerente deve ver todas as seis linhas. Os usuários Vendas1 e Vendas2 deverão ver apenas suas próprias vendas.

Altere a política de segurança para desabilitar a política específica.

```sql
ALTER SECURITY POLICY SalesFilter  
WITH (STATE = OFF);  
```

Agora, os usuários Vendas1 e Vendas2 podem ver todas as seis linhas.

Conectar-se ao banco de dados SQL para limpar recursos

```sql
DROP USER Sales1;
DROP USER Sales2;
DROP USER Manager;

DROP SECURITY POLICY SalesFilter;
DROP TABLE Sales;
DROP FUNCTION Security.fn_securitypredicate;
DROP SCHEMA Security;
```

### <a name="b-scenarios-for-using-row-level-security-on-an-azure-sql-data-warehouse-external-table"></a><a name="external"></a> B. Cenários de uso de Segurança em Nível de Linha em uma tabela externa do SQL Data Warehouse do Azure

Esse pequeno exemplo cria três usuários e uma tabela externa com seis linhas. Em seguida, ele cria uma função com valor de tabela embutida e uma política de segurança para a tabela externa. O exemplo mostra como as instruções select são filtrados para os diversos usuários.

Crie três contas de usuário que demonstrem os diferentes recursos de acesso.

```sql
CREATE LOGIN Manager WITH PASSWORD = 'somepassword'
GO
CREATE LOGIN Sales1 WITH PASSWORD = 'somepassword'
GO
CREATE LOGIN Sales2 WITH PASSWORD = 'somepassword'
GO

CREATE USER Manager FOR LOGIN Manager;  
CREATE USER Sales1  FOR LOGIN Sales1;  
CREATE USER Sales2  FOR LOGIN Sales2 ;
```

Crie uma tabela para armazenar dados.  

```sql
CREATE TABLE Sales  
    (  
    OrderID int,  
    SalesRep sysname,  
    Product varchar(10),  
    Qty int  
    );  
```

Preencha a tabela com seis linhas de dados, mostrando três pedidos para cada representante de vendas.  

```sql
INSERT INTO Sales VALUES (1, 'Sales1', 'Valve', 5);
INSERT INTO Sales VALUES (2, 'Sales1', 'Wheel', 2);
INSERT INTO Sales VALUES (3, 'Sales1', 'Valve', 4);
INSERT INTO Sales VALUES (4, 'Sales2', 'Bracket', 2);
INSERT INTO Sales VALUES (5, 'Sales2', 'Wheel', 5);
INSERT INTO Sales VALUES (6, 'Sales2', 'Seat', 5);
-- View the 6 rows in the table  
SELECT * FROM Sales;
```

Crie uma tabela externa do SQL Data Warehouse do Azure na tabela de Vendas criada.

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'somepassword';

CREATE DATABASE SCOPED CREDENTIAL msi_cred WITH IDENTITY = 'Managed Service Identity';

CREATE EXTERNAL DATA SOURCE ext_datasource_with_abfss WITH (TYPE = hadoop, LOCATION = 'abfss://myfile@mystorageaccount.dfs.core.windows.net', CREDENTIAL = msi_cred);

CREATE EXTERNAL FILE FORMAT MSIFormat  WITH (FORMAT_TYPE=DELIMITEDTEXT);
  
CREATE EXTERNAL TABLE Sales_ext WITH (LOCATION='RLSExtTabletest.tbl', DATA_SOURCE=ext_datasource_with_abfss, FILE_FORMAT=MSIFormat, REJECT_TYPE=Percentage, REJECT_SAMPLE_VALUE=100, REJECT_VALUE=100)
AS SELECT * FROM sales;
```

Conceda SELECT para a tabela externa de três usuários.

```sql
GRANT SELECT ON Sales_ext TO Sales1;  
GRANT SELECT ON Sales_ext TO Sales2;  
GRANT SELECT ON Sales_ext TO Manager;
```

Crie uma política de segurança na tabela externa usando a função na sessão A como um predicado de filtro. O estado deve ser definido como ON para habilitar a política.

```sql
CREATE SECURITY POLICY SalesFilter_ext
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesRep)
ON dbo.Sales_ext  
WITH (STATE = ON);
```

Agora teste o predicado de filtragem selecionando a tabela externa Sales_ext. Faça login como cada usuário: Vendas1, Vendas2 e Gerente. Execute o comando a seguir como cada usuário.

```sql
SELECT * FROM Sales_ext;
```

O gerente deve ver todas as seis linhas. Os usuários Vendas1 e Vendas2 deverão ver apenas suas vendas.

Altere a política de segurança para desabilitar a política específica.

```sql
ALTER SECURITY POLICY SalesFilter_ext  
WITH (STATE = OFF);  
```

Agora, os usuários Vendas1 e Vendas2 podem ver todas as seis linhas.

Conectar ao banco de dados do SQL Data Warehouse para limpar recursos

```sql
DROP USER Sales1;
DROP USER Sales2;
DROP USER Manager;

DROP SECURITY POLICY SalesFilter_ext;
DROP TABLE Sales;
DROP EXTERNAL TABLE Sales_ext;
DROP EXTERNAL DATA SOURCE ext_datasource_with_abfss ;
DROP EXTERNAL FILE FORMAT MSIFormat;
DROP DATABASE SCOPED CREDENTIAL msi_cred; 
DROP MASTER KEY;
```

Conecte-se com o mestre lógico para limpar os recursos.

```sql
DROP LOGIN Sales1;
DROP LOGIN Sales2;
DROP LOGIN Manager;
```

### <a name="c-scenario-for-users-who-connect-to-the-database-through-a-middle-tier-application"></a><a name="MidTier"></a> C. Cenário para usuários que se conectam ao banco de dados por meio de um aplicativo de camada intermediária

> [!NOTE]
> Neste exemplo, atualmente a função de predicados de bloco não é compatível com o SQL Data Warehouse do Azure, portanto, a inserção de linhas para o ID de usuário errado não é bloqueada no Azure SQL Data Warehouse.

Este exemplo mostra como um aplicativo de camada intermediária pode implementar a filtragem de conexão, onde os usuários do aplicativo (ou locatários) compartilham o mesmo usuário de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o aplicativo). O aplicativo define a ID do usuário do aplicativo atual em [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md) depois de se conectar ao banco de dados e, em seguida, as políticas de segurança filtram de modo transparente as linhas que não devem ficar visíveis para essa ID, além de impedir o usuário de inserir linhas para a ID de usuário incorreta. Não é necessária nenhuma outra alteração de aplicativo.  
  
 Crie uma tabela para armazenar dados.

```sql
CREATE TABLE Sales (  
    OrderId int,  
    AppUserId int,  
    Product varchar(10),  
    Qty int  
);  
```

Preencha a tabela com seis linhas de dados, mostrando três pedidos para cada usuário do aplicativo.

```sql
INSERT Sales VALUES
    (1, 1, 'Valve', 5),
    (2, 1, 'Wheel', 2),
    (3, 1, 'Valve', 4),  
    (4, 2, 'Bracket', 2),
    (5, 2, 'Wheel', 5),
    (6, 2, 'Seat', 5);  
```

Crie um usuário de privilégio baixo que o aplicativo usará para se conectar.

```sql
-- Without login only for demo  
CREATE USER AppUser WITHOUT LOGIN;
GRANT SELECT, INSERT, UPDATE, DELETE ON Sales TO AppUser;  
  
-- Never allow updates on this column  
DENY UPDATE ON Sales(AppUserId) TO AppUser;  
```

Crie um novo esquema e função de predicado, que usarão a ID de usuário do aplicativo armazenada em **SESSION_CONTEXT** para filtrar as linhas.

```sql
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@AppUserId int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result  
    WHERE  
        DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('AppUser')
        AND CAST(SESSION_CONTEXT(N'UserId') AS int) = @AppUserId;
GO  
```

Crie uma política de segurança que adicione essa função como um predicado de filtro e um predicado de bloqueio em `Sales`. O predicado de bloqueio precisa apenas de **AFTER INSERT**, pois **BEFORE UPDATE** e **BEFORE DELETE** já foram filtrados e **AFTER UPDATE** é desnecessário, pois a coluna `AppUserId` não pode ser atualizada para outros valores, devido à permissão de coluna definida anteriormente.

```sql
CREATE SECURITY POLICY Security.SalesFilter  
    ADD FILTER PREDICATE Security.fn_securitypredicate(AppUserId)
        ON dbo.Sales,  
    ADD BLOCK PREDICATE Security.fn_securitypredicate(AppUserId)
        ON dbo.Sales AFTER INSERT
    WITH (STATE = ON);  
```

Agora você pode simular a filtragem de conexão selecionando na tabela `Sales` após definição de IDs de usuário diferentes em **SESSION_CONTEXT**. Na prática, o aplicativo é responsável por definir a ID do usuário atual em **SESSION_CONTEXT** depois de abrir uma conexão.

```sql
EXECUTE AS USER = 'AppUser';  
EXEC sp_set_session_context @key=N'UserId', @value=1;  
SELECT * FROM Sales;  
GO  
  
/* Note: @read_only prevents the value from changing again until the connection is closed (returned to the connection pool)*/
EXEC sp_set_session_context @key=N'UserId', @value=2, @read_only=1;
  
SELECT * FROM Sales;  
GO  
  
INSERT INTO Sales VALUES (7, 1, 'Seat', 12); -- error: blocked from inserting row for the wrong user ID  
GO  
  
REVERT;  
GO  
```

Limpe os recursos de banco de dados.

```sql
DROP USER AppUser;

DROP SECURITY POLICY Security.SalesFilter;
DROP TABLE Sales;
DROP FUNCTION Security.fn_securitypredicate;
DROP SCHEMA Security;
```

## <a name="see-also"></a>Consulte Também

 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)</br>
 [ALTER SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)</br>
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)</br>
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)</br>
 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)</br>
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)</br>
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)</br>
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)</br>
 [Criar funções definidas pelo usuário &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)
