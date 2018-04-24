---
title: Segurança em nível de linha | Microsoft Docs
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- access control predicates
- row level security
- security [SQL Server], predicate based access control
- row level security described
- predicate based security
ms.assetid: 7221fa4e-ca4a-4d5c-9f93-1b8a4af7b9e8
caps.latest.revision: 47
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a07ccc6c625a36846c19add5733202950b24e76b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="row-level-security"></a>Segurança em nível de linha
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  ![Gráfico de segurança em nível de linha](../../relational-databases/security/media/row-level-security-graphic.png "Gráfico de segurança em nível de linha")  
  
 Segurança em nível de linha permite aos clientes controlar o acesso às linhas em uma tabela de banco de dados com base nas características do usuário executando uma consulta (por exemplo, associação a grupo ou contexto de execução).  
  
 O RLS (nível de linha de segurança) simplifica o design e a codificação de segurança em seu aplicativo. O RLS permite a você implementar restrições de acesso a linhas de dados. Por exemplo, garantindo que os funcionários possam acessar somente as linhas de dados que são relevantes para seu departamento ou restringir o acesso do cliente a somente aos dados relevantes para a empresa desse cliente.  
  
 A lógica de restrição de acesso é localizado na camada de banco de dados, em vez de longe dos dados em outra camada de aplicativo. O sistema de banco de dados aplica as restrições de acesso toda vez que há tentativa de acesso a dados a partir de qualquer camada. Isso torna o sistema de segurança mais robusto e confiável, reduzindo a área de superfície do seu sistema de segurança.  
  
 Implemente a RLS usando a instrução [CREATE SECURITY POLICY](../../t-sql/statements/create-security-policy-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] e predicados criados como [funções com valor de tabela embutida](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md).  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Obter](http://azure.micosoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).  
  

##  <a name="Description"></a> Descrição  
 A RLS permite dois tipos de predicado de segurança.  
  
-   Os predicados de filtro filtram silenciosamente as linhas disponíveis para operações de leitura (SELECT, UPDATE e DELETE).  
  
-   Os predicados de bloqueio bloqueiam explicitamente as operações de gravação (AFTER INSERT, AFTER UPDATE, BEFORE UPDATE, BEFORE DELETE) que violam o predicado.  
  
 O acesso aos dados no nível de linha em uma tabela é restrito por um predicado de segurança definido como uma função com valor de tabela embutida. A função é então invocada e imposta por uma política de segurança. Para predicados de filtro, não há nenhuma indicação ao aplicativo de que as linhas tenham sido filtradas no conjunto de resultados; se todas as linhas forem filtradas, um conjunto de null será retornado. Para predicados de bloqueio, todas as operações que violem o predicado falharão com um erro.  
  
 Os predicados de filtro são aplicados durante a leitura de dados da tabela base e ela afeta todas as operações get: **SELECT**, **DELETE** (ou seja, o usuário não pode excluir linhas que são filtradas) e **UPDATE** (ou seja, o usuário não pode atualizar as linhas que são filtradas, embora seja possível atualizar as linhas de modo que sejam filtradas subsequentemente). Os predicados de bloqueio afetam todas as operações de gravação.  
  
-   Os predicados AFTER INSERT e AFTER UPDATE podem impedir que os usuários atualizem linhas para valores que violem o predicado.  
  
-   Os predicados BEFORE UPDATE podem impedir que os usuários atualizem linhas que atualmente violem o predicado.  
  
-   Os predicados BEFORE DELETE podem bloquear operações de exclusão.  
  
 Os predicados de filtro e bloqueio, bem como as políticas de segurança têm o seguinte comportamento:  
  
-   Você pode definir uma função de predicado que se une a outra tabela e/ou invoca uma função. Se a política de segurança for criada com `SCHEMABINDING = ON`, a junção ou a função será acessível pela consulta e funciona como esperado, sem nenhuma verificação de permissão adicional. Se a política de segurança for criada com `SCHEMABINDING = OFF`, os usuários precisarão ter permissões **SELECT** ou **EXECUTE** nessas tabelas e funções adicionais para consultar a tabela de destino.
  
-   Você pode fazer uma consulta em uma tabela que tenha um predicado de segurança definido mas desabilitado. Quaisquer linhas que tenham sido filtradas ou bloqueadas não serão afetadas.  
  
-   Se o usuário dbo, um membro da função **db_owner** ou o proprietário da tabela fizer uma consulta em uma tabela que tem uma política de segurança definida e habilitada, as linhas serão filtradas ou bloqueadas conforme definido pela política de segurança.  
  
-   As tentativas de alterar o esquema de uma tabela associada por uma política de segurança associada ao esquema resultarão em um erro. No entanto, as colunas não referenciadas pelo predicado podem ser alteradas.  
  
-   As tentativas de adicionar um predicado em uma tabela que já tenha um definido para a operação especificada (independentemente de ele estar habilitado ou desabilitado) resultarão em um erro.  
  
-   Para políticas de segurança associadas ao esquema, as tentativas de modificar uma função usada como um predicado em uma tabela em uma política de segurança resultarão em um erro.  
  
-   Definir múltiplas políticas de segurança ativas que contêm predicados não sobrepostos é uma ação que terá êxito.  
  
 Os predicados de filtro apresentam o seguinte comportamento:  
  
-   Defina uma política de segurança que filtra as linhas de uma tabela. O aplicativo não fica ciente de que todas as linhas foram filtradas para as operações **SELECT**, **UPDATE**e **DELETE** , incluindo situações em que todas as linhas tiverem sido filtradas. O aplicativo pode **INSERT** quaisquer linhas, independentemente de estas serem ou não filtradas futuramente, durante qualquer outra operação.  
  
 Os predicados de bloqueio apresentam o seguinte comportamento:  
  
-   Os predicados de bloqueio para UPDATE são divididos em operações distintas para BEFORE e AFTER. Consequentemente, não é possível, por exemplo, impedir os usuários de atualizar uma linha para ter um valor maior que o atual. Se esse tipo de lógica for necessário, você deverá usar gatilhos com as tabelas intermediárias DELETED e INSERTED para fazer referência a valores novos e antigos juntos.  
  
-   O otimizador não verificará um predicado de bloqueio AFTER UPDATE se nenhuma das colunas usadas pela função de predicado tiver sido alterada. Por exemplo, Alice não deve poder alterar um salário para acima de 100.000, mas deve poder alterar o endereço de um funcionário cujo salário já seja superior a 100.000 (e, desse modo, já viola o predicado).  
  
-   Nenhuma mudança foi feita nas APIs em massa, incluindo BULK INSERT. Isso significa que os predicados de bloqueio AFTER INSERT serão aplicados às operações de inserção em massa, assim como seriam em operações de inserção regular.  
  
  
##  <a name="UseCases"></a> Casos de uso  
 Estes são exemplos de design de como RLS pode ser usado:  
  
-   Um hospital pode criar uma diretiva de segurança que permite a enfermeiras exibir linhas de dados somente para seus próprios pacientes.  
  
-   Um banco pode criar uma política para restringir o acesso a linhas de dados financeiros com base na divisão de negócios do funcionário, ou com base na função desempenhada pelo funcionário na empresa.  
  
-   Um aplicativo multilocatário pode criar uma política para impor uma separação lógica entre as linhas de dados de cada locatário e as linhas referentes a todos os outros locatários. Eficiência é obtida pelo armazenamento de dados para vários locatários em uma única tabela. Obviamente, cada locatário pode ver somente as linhas com seus próprios dados.  
  
 Os predicados de filtro RLS são funcionalmente equivalentes a acrescentar uma cláusula **WHERE** . O predicado pode ser tão sofisticado como ditam as práticas comerciais, ou a cláusula pode ser tão simples quanto `WHERE TenantId = 42`.  
  
 Em termos mais formais, o RLS introduz o controle de acesso baseado em predicado. Ele apresenta uma avaliação centralizada, flexível e baseada em predicado que pode levar em consideração metadados ou quaisquer outros critérios que o administrador determina conforme apropriado. O predicado é usado como critério para determinar se o usuário tem acesso apropriado aos dados com base em atributos de usuário. Controle de acesso baseado em rótulos pode ser implementado usando o controle de acesso baseado em predicado.  
  
  
##  <a name="Permissions"></a> Permissões  
 Criando, alterando ou removendo políticas de segurança requer a permissão **ALTER ANY SECURITY POLICY** . Criar ou descartar uma política de segurança requer a permissão **ALTER** no esquema.  
  
 Além disso, as seguintes permissões são necessárias para cada predicado que é adicionado:  
  
-   Permissões**SELECT** e **REFERENCES** na função que está sendo usada como um predicado.  
  
-   Permissão**REFERENCES** na tabela de destino que está sendo associada à política.  
  
-   permissão**REFERENCES** em todas as colunas da tabela de destino usadas como argumentos.  
  
 Diretivas de segurança se aplicam a todos os usuários, incluindo usuários de dbo do banco de dados. Os usuários do dbo podem alterar ou descartar as políticas de segurança, mas suas alterações às políticas de segurança podem ser auditadas. Se os usuários com altos privilégios (como sysadmin ou db_owner) precisarem ver todas as linhas para solucionar problemas ou validar dados, a política de segurança deverá ser escrita para permitir isso.  
  
 Se uma política de segurança for criada com `SCHEMABINDING = OFF`, para consultar a tabela de destino, os usuários deverão ter a permissão  **SELECT** ou **EXECUTE** na função de predicado e em todas as tabelas, exibições ou funções usadas adicionais na função de predicado. Se uma política de segurança for criada com `SCHEMABINDING = ON` (o padrão), essas verificações de permissão serão ignoradas quando os usuários consultarem a tabela de destino.  
  
  
##  <a name="Best"></a> Práticas recomendadas  
  
-   É altamente recomendável criar um esquema separado para os objetos RLS (função de predicado e política de segurança).  
  
-   A permissão **ALTER ANY SECURITY POLICY** é destinada a usuários altamente privilegiados (como um gerente de políticas de segurança). O Gerenciador de políticas de segurança não exige permissão **SELECT** nas tabelas que ele protege.  
  
-   Evite conversões de tipo em funções de predicado para evitar possíveis erros de tempo de execução.  
  
-   Evite a recursão no predicado funções sempre que possível para evitar a degradação do desempenho. O otimizador de consulta tentará detectar recursões diretas, mas não há garantia de que encontrará recursões indiretas (isto é, onde uma segunda função chama a função de predicado).  
  
-   Evite usar junções de tabelas em excesso em funções de predicado, para maximizar o desempenho.  
  
 Evite a lógica de predicado que depende de [opções SET](../../t-sql/statements/set-statements-transact-sql.md)específicas da sessão: embora seja improvável que elas sejam usadas em aplicações práticas, as funções de predicado cuja lógica depende de determinadas opções **SET** específicas da sessão poderão perder informações se os usuários conseguirem executar consultas arbitrárias. Por exemplo, uma função de predicado que implicitamente converte uma cadeia de caracteres em **datetime** poderia filtrar linhas diferentes com base na opção **SET DATEFORMAT** da sessão atual. Em geral, as funções de predicado devem obedecer as regras a seguir:  
  
-   As funções de predicado não devem converter implicitamente cadeias de caracteres em **date**, **smalldatetime**, **datetime**, **datetime2** ou **datetimeoffset**, ou vice-versa, pois essas conversões são afetadas pleas opções [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md) e [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md). Em vez disso, use a função **CONVERT** e especifique explicitamente o parâmetro de estilo.  
  
-   As funções de predicado não devem se basear no valor do primeiro dia da semana, pois esse valor é afetado pela opção [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).  
  
-   As funções de predicado não devem se basear em expressões aritméticas ou de agregação que retornam **NULL** em caso de erro (como um estouro ou divisão por zero), pois esse comportamento é afetado pelas opções [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md), [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md) e [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md).  
  
-   As funções de predicado não devem comparar cadeias de caracteres concatenadas com **NULL**, pois esse comportamento é afetado pela opção [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
   
  
##  <a name="SecNote"></a> Observação de segurança: ataques de canal lateral  
 **Gerenciador de políticas de segurança mal-intencionado:** é importante observar que um gerenciador de políticas de segurança mal-intencionado com permissões suficientes para criar uma política de segurança sobre uma coluna confidencial e que tenha permissão para criar ou alterar funções com valor de tabela embutida poderá pactuar com outro usuário que tenha permissões SELECT em uma tabela para realizar a exfiltração de dados pela criação maliciosa de funções com valor de tabela embutida, concebidas para utilizar ataques de canal lateral com o objetivo de inferir dados. Esses ataques exigiriam a colusão (ou excesso de permissões concedidas a um usuário mal-intencionado) e provavelmente demandariam várias iterações de modificação da política (exigindo permissão para remover o predicado, para que pudessem então quebrar a ligação do esquema), modificando as funções embutidas com valor de tabela e repetidamente executando instruções SELECT na tabela de destino. É altamente recomendável limitar as permissões conforme necessário e monitorar quaisquer atividades suspeitas, como mudança constante de políticas e funções embutidas com valor de tabela relacionadas à segurança de nível de linha.  
  
 **Consultas cuidadosamente concebidas:** é possível causar vazamento de informações pelo uso de consultas concebidas cuidadosamente. Por exemplo, `SELECT 1/(SALARY-100000) FROM PAYROLL WHERE NAME='John Doe'` permitiria que um usuário mal-intencionado soubesse que o salário de John Doe é US$ 100.000. Mesmo que haja um predicado de segurança em vigor para impedir que um usuário mal-intencionado consulte diretamente o salário de outras pessoas, o usuário pode determinar quando a consulta retorna uma exceção de divisão por zero.  
   
  
##  <a name="Limitations"></a> Compatibilidade entre recursos  
 De modo geral, a segurança no nível de linha funcionará conforme o esperado entre os recursos. No entanto, há algumas exceções. Esta seção documenta várias observações e limitações para o uso da segurança em nível de linha com determinados recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **DBCC SHOW_STATISTICS** relata estatísticas de dados não filtrados e, portanto, pode perder informações que, de outra forma, estariam protegidas por uma política de segurança. Por esse motivo, para exibir um objeto estatístico de uma tabela com uma política de segurança no nível de linha, o usuário deve ter ser proprietário da tabela ou deve ser um membro da função de servidor fixa de sysadmin, da função de banco de dados fixa db_owner ou da função de banco de dados fixa db_ddladmin.  
  
-   **Filestream** A RLS não é compatível com Filestream.  
  
-   **Polybase** A RLS não é compatível com o Polybase.  
  
-   **Tabelas com Otimização de Memória**A função com valor de tabela embutida usada como um predicado de segurança em uma tabela com otimização de memória deve ser definida usando a opção `WITH NATIVE_COMPILATION` . Com essa opção, os recursos de linguagem não permitidos pelas tabelas com otimização de memória serão banidos e o erro apropriado será emitido no momento da criação. Para obter mais informações, veja a seção **Segurança em nível de linha em tabelas com otimização de memória** em [Introdução às tabelas com otimização de memória](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md).  
  
-   **Exibições indexadas** De modo geral, as políticas de segurança podem ser criadas sobre as exibições, e as exibições podem ser criadas sobre as tabelas que são associadas pelas políticas de segurança. No entanto, as exibições indexadas não podem ser criadas sobre as tabelas que têm uma política de segurança, pois as pesquisas de linha pelo índice contornariam a política.  
  
-   **Captura de Dados de Alteração** A Captura de Dados de Alteração pode perder linhas inteiras que devem ser filtradas para membros do **db_owner** ou para usuários que são membros da função “gating” especificada quando a CDC é habilitada para uma tabela (observação: você pode definir explicitamente isso para **NULL** a fim de permitir que todos os usuários acessem os dados alterados). Na verdade, **db_owner** e os membros dessa função gating poderão ver todas as alterações nos dados de uma tabela, mesmo se houver uma política de segurança na tabela.  
  
-   **Controle de Alterações** O Controle de Alterações pode deixar vazar a chave primária de linhas que deve ser filtrada para usuários com as permissões **SELECT** e **VIEW CHANGE TRACKING** . Os valores de dados reais não vazam; apenas o fato de que a coluna A foi atualizada/inserida/excluída para a linha com a chave primária B. Isso será um problema se a chave primária contiver um elemento confidencial, como um Número de Seguro Social. No entanto, na prática, esse **CHANGETABLE** é quase sempre unido à tabela original para obtenção de dados mais recentes.  
  
-   **Pesquisa de Texto Completo** Uma queda no desempenho é esperada em consultas que usam as funções de Pesquisa de Texto Completo e Pesquisa Semântica devido a uma junção extra apresentada para aplicar a segurança em nível de linha e evitar a perda das chaves primárias de linhas que devem ser filtradas: **CONTAINSTABLE**, **FREETEXTTABLE**, semantickeyphrasetable, semanticsimilaritydetailstable, semanticsimilaritytable.  
  
-   **Índices Columnstore** A RLS é compatível com índices columnstore clusterizados e não clusterizados. No entanto, como a segurança no nível de linha se aplica a uma função, é possível que o otimizador possa modificar o plano de consulta, de modo que ele não use o modo de lote.  
  
-   **Exibições Particionadas** Os predicados de bloqueio não podem ser definidos em exibições particionadas, e as exibições particionadas não podem ser criadas sobre as tabelas que usam predicados de bloqueio. Os predicados de filtro são compatíveis com exibições particionadas.  
  
-   As**tabelas temporais** são compatíveis com a RLS. No entanto, os predicados de segurança na tabela atual não são replicados automaticamente na tabela de histórico. Para aplicar uma política de segurança às tabelas atual e de histórico, você deverá adicionar individualmente um predicado de segurança em cada tabela.  
  
  
##  <a name="CodeExamples"></a> Exemplos  
  
###  <a name="Typical"></a> A. Cenário para usuários que se autenticam no banco de dados  
 Esse pequeno exemplo cria três usuários, cria e preenche uma tabela com 6 linhas e cria também uma função de valor de tabela embutida, e uma política de segurança para essa tabela. O exemplo mostra como as instruções select são filtrados para os diversos usuários.  
  
 Crie três contas de usuário que demonstrem os diferentes recursos de acesso.  
  
```sql  
CREATE USER Manager WITHOUT LOGIN;  
CREATE USER Sales1 WITHOUT LOGIN;  
CREATE USER Sales2 WITHOUT LOGIN;  
```  
  
 Crie uma tabela simples para armazenar dados.  
  
```  
CREATE TABLE Sales  
    (  
    OrderID int,  
    SalesRep sysname,  
    Product varchar(10),  
    Qty int  
    );  
```  
  
 Preencha a tabela com 6 linhas de dados, mostrando 3 pedidos para cada representante de vendas.  
  
```  
INSERT Sales VALUES   
(1, 'Sales1', 'Valve', 5),   
(2, 'Sales1', 'Wheel', 2),   
(3, 'Sales1', 'Valve', 4),  
(4, 'Sales2', 'Bracket', 2),   
(5, 'Sales2', 'Wheel', 5),   
(6, 'Sales2', 'Seat', 5);  
-- View the 6 rows in the table  
SELECT * FROM Sales;  
```  
  
 Conceda acesso de leitura à tabela para cada usuário.  
  
```  
GRANT SELECT ON Sales TO Manager;  
GRANT SELECT ON Sales TO Sales1;  
GRANT SELECT ON Sales TO Sales2;  
```  
  
 Crie um novo esquema e uma função de valor de tabela embutida. A função retorna 1 quando uma linha da coluna do representante de vendas é o mesmo que o usuário que executa a consulta (`@SalesRep = USER_NAME()`) ou se o usuário executando a consulta for o gerente (`USER_NAME() = 'Manager'`).  
  
```  
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
  
```  
CREATE SECURITY POLICY SalesFilter  
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesRep)   
ON dbo.Sales  
WITH (STATE = ON);  
```  
  
 Agora teste o predicado de filtragem selecionando-o a partir da tabela Vendas como cada usuário.  
  
```  
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
  
 O gerente deve ver todas as 6 linhas. Os usuários Vendas1 e Vendas2 deverão ver apenas suas próprias vendas.  
  
 Altere a política de segurança para desabilitar a política específica.  
  
```  
ALTER SECURITY POLICY SalesFilter  
WITH (STATE = OFF);  
```  
  
 Agora os usuários Vendas1 e Vendas2 podem ver todas as 6 linhas.  
  
  
###  <a name="MidTier"></a> B. Cenário para usuários que se conectam ao banco de dados por meio de um aplicativo de camada intermediária  
 Este exemplo mostra como um aplicativo de camada intermediária pode implementar a filtragem de conexão, onde os usuários do aplicativo (ou locatários) compartilham o mesmo usuário de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o aplicativo). O aplicativo define a ID do usuário do aplicativo atual em [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md) depois de se conectar ao banco de dados e, em seguida, as políticas de segurança filtram de modo transparente as linhas que não devem ficar visíveis para essa ID, além de impedir o usuário de inserir linhas para a ID de usuário incorreta. Não é necessária nenhuma outra alteração no aplicativo.  
  
 Crie uma tabela simples para armazenar dados.  
  
```  
CREATE TABLE Sales (  
    OrderId int,  
    AppUserId int,  
    Product varchar(10),  
    Qty int  
);  
```  
  
 Preencha a tabela com 6 linhas de dados mostrando 3 pedidos para cada usuário do aplicativo.  
  
```  
INSERT Sales VALUES   
    (1, 1, 'Valve', 5),   
    (2, 1, 'Wheel', 2),   
    (3, 1, 'Valve', 4),  
    (4, 2, 'Bracket', 2),   
    (5, 2, 'Wheel', 5),   
    (6, 2, 'Seat', 5);  
```  
  
 Crie um usuário de privilégio baixo que o aplicativo usará para se conectar.  
  
```  
-- Without login only for demo  
CREATE USER AppUser WITHOUT LOGIN;   
GRANT SELECT, INSERT, UPDATE, DELETE ON Sales TO AppUser;  
  
-- Never allow updates on this column  
DENY UPDATE ON Sales(AppUserId) TO AppUser;  
```  
  
 Crie um novo esquema e função de predicado, que usarão a ID de usuário do aplicativo armazenada em **SESSION_CONTEXT** para filtrar as linhas.  
  
```  
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
  
```  
CREATE SECURITY POLICY Security.SalesFilter  
    ADD FILTER PREDICATE Security.fn_securitypredicate(AppUserId)   
        ON dbo.Sales,  
    ADD BLOCK PREDICATE Security.fn_securitypredicate(AppUserId)   
        ON dbo.Sales AFTER INSERT   
    WITH (STATE = ON);  
```  
  
 Agora você pode simular a filtragem de conexão selecionando na tabela `Sales` após definição de IDs de usuário diferentes em **SESSION_CONTEXT**. Na prática, o aplicativo é responsável por definir a ID do usuário atual em **SESSION_CONTEXT** depois de abrir uma conexão.  
  
```  
EXECUTE AS USER = 'AppUser';  
EXEC sp_set_session_context @key=N'UserId', @value=1;  
SELECT * FROM Sales;  
GO  
  
--  Note: @read_only prevents the value from changing again   
--  until the connection is closed (returned to the connection pool)  
EXEC sp_set_session_context @key=N'UserId', @value=2, @read_only=1;   
  
SELECT * FROM Sales;  
GO  
  
INSERT INTO Sales VALUES (7, 1, 'Seat', 12); -- error: blocked from inserting row for the wrong user ID  
GO  
  
REVERT;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [ALTER SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [Criar funções definidas pelo usuário &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)  
  
  
