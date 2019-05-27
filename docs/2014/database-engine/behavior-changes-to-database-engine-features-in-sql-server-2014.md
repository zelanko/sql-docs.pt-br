---
title: Recursos no SQL Server 2014 do mecanismo de banco de dados de alterações de comportamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- behavior changes [SQL Server]
- Database Engine [SQL Server], what's new
- Transact-SQL behavior changes
ms.assetid: 65eaafa1-9e06-4264-b547-cbee8013c995
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6e7b629b93e0c79a003019a2e024388d54b12b76
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065209"
---
# <a name="behavior-changes-to-database-engine-features-in-sql-server-2014"></a>Alterações no comportamento de recursos do Mecanismo de Banco de Dados no SQL Server 2014
  Este tópico descreve as alterações no comportamento no [!INCLUDE[ssDE](../includes/ssde-md.md)]. Essas alterações afetam a maneira como os recursos funcionam ou interagem no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] em comparação com as versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="behavior-changes-in-includesssql14includessssql14-mdmd"></a>Alterações de comportamento no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], as consultas em um documento XML que contém cadeias de caracteres em um determinado comprimento (mais de 4020 caracteres) podem retornar resultados incorretos. No [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], tais consultas retornam os resultados corretos.  
  
## <a name="behavior-changes-in-includesssql11includessssql11-mdmd"></a>Alterações de comportamento no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="metadata-discovery"></a>Descoberta de metadados  
 Melhorias na [!INCLUDE[ssDE](../includes/ssde-md.md)] começando com [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] permitir SQLDescribeCol Obtenha descrições mais precisas dos resultados esperados que os retornados por SQLDescribeCol nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Descoberta de metadados](../relational-databases/native-client/features/metadata-discovery.md).  
  
 O [SET FMTONLY](/sql/t-sql/statements/set-fmtonly-transact-sql) opção para determinar o formato de uma resposta sem realmente executar a consulta é substituído pelo [sp_describe_first_result_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql), [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql), [DM exec_describe_first_result_set &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql), e [sys exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql).  
  
### <a name="changes-to-behavior-in-scripting-a-sql-server-agent-task"></a>Alterações de comportamento ao gerar scripts de uma tarefa do SQL Server Agent  
 No [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], se você criar um novo trabalho copiando o script de um trabalho existente, o novo trabalho poderá afetar inadvertidamente o trabalho existente. Para criar um novo trabalho usando o script de um trabalho existente, exclua manualmente o parâmetro *@schedule_uid* que geralmente é o último parâmetro da seção que cria a agenda de trabalho no trabalho existente. Isso criará uma nova agenda independente para o novo trabalho sem afetar os trabalhos existentes.  
  
### <a name="constant-folding-for-clr-user-defined-functions-and-methods"></a>Dobra constante para funções e métodos de CLR definidos pelo usuário  
 No [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], os objetos CLR definidos pelo usuário a seguir agora são dobráveis:  
  
-   Funções definidas pelo usuário de CLR com valor escalar determinista.  
  
-   Métodos deterministas de tipos de CLR definidos pelo usuário.  
  
 Esta melhoria busca aprimorar o desempenho quando estas funções ou métodos são chamados mais de uma vez com os mesmos argumentos. Porém, esta alteração pode causar resultados inesperados quando funções ou métodos não deterministas são marcados como deterministas em erro. O determinismo de uma função ou um método CLR é indicado pelo valor da propriedade `IsDeterministic` de `SqlFunctionAttribute` ou `SqlMethodAttribute`.  
  
### <a name="behavior-of-stenvelope-method-has-changed-with-empty-spatial-types"></a>O comportamento do método STEnvelope() mudou com tipos espaciais vazios  
 Agora o comportamento do método `STEnvelope` com objetos vazios é consistente com o comportamento de outros métodos espaciais do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], o método `STEnvelope` retornou os seguintes resultados quando chamado com objetos vazios:  
  
```  
select geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns POINT EMPTY  
select geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns LINESTRING EMPTY  
select geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns POLYGON EMPTY  
```  
  
 No [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], o método `STEnvelope` agora retorna os seguintes resultados quando chamado com objetos vazios:  
  
```  
select geometry::Parse('POINT EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
select geometry::Parse('LINESTRING EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
select geometry::Parse('POLYGON EMPTY').STEnvelope().ToString()  
-- returns GEOMETRYCOLLECTION EMPTY  
```  
  
 Para determinar se um objeto espacial é vazio, chame o [STIsEmpty &#40;tipo de dados geometry&#41; ](/sql/t-sql/spatial-geometry/stisempty-geometry-data-type) método.  
  
### <a name="log-function-has-new-optional-parameter"></a>A função LOG tem novo parâmetro opcional  
 O `LOG` função agora tem um recurso opcional *base* parâmetro. Para obter mais informações, consulte [LOG &#40;Transact-SQL&#41;](/sql/t-sql/functions/log-transact-sql).  
  
### <a name="statistics-computation-during-partitioned-index-operations-has-changed"></a>A computação de estatísticas durante operações de índice particionado mudou  
 No [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], as estatísticas não são criadas por meio do exame de todas as linhas da tabela quando um índice particionado é criado ou reconstruído. Em vez disso, o otimizador de consultas usa o algoritmo de amostragem padrão para gerar estatísticas. Depois de atualizar um banco de dados com índices particionados, você pode notar uma diferença nos dados de histograma destes índices. Esta alteração no comportamento pode não afetar o desempenho de consulta. Para obter estatísticas em índices particionados por meio do exame de todas as linhas da tabela, use CREATE STATISTICS ou UPDATE STATISTICS com a cláusula FULLSCAN.  
  
### <a name="data-type-conversion-by-the-xml-value-method-has-changed"></a>A conversão de tipo de dados pelo método de valor XML mudou  
 O comportamento interno do método `value` do tipo de dados `xml` mudou. Este método executa um XQuery no XML e retorna um valor escalar do tipo de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificado. O tipo xs tem de ser convertido no tipo de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Anteriormente, o método `value` convertia internamente o valor de origem em xs:string e depois convertia xs:string no tipo de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], a conversão em xs:string é ignorada nos seguintes casos:  
  
|Tipo de dados de origem XS|Tipo de dados de destino do SQL Server|  
|-------------------------|--------------------------------------|  
|byte<br /><br /> short<br /><br /> INT<br /><br /> inteiro<br /><br /> long<br /><br /> unsignedByte<br /><br /> unsignedShort<br /><br /> unsignedInt<br /><br /> unsignedLong<br /><br /> positiveInteger<br /><br /> nonPositiveInteger<br /><br /> negativeInteger<br /><br /> nonNegativeInteger|TINYINT<br /><br /> SMALLINT<br /><br /> INT<br /><br /> BIGINT<br /><br /> Decimal<br /><br /> numeric|  
|Decimal|Decimal<br /><br /> numeric|  
|FLOAT|REAL|  
|double|FLOAT|  
  
 O novo comportamento melhora o desempenho quando a conversão intermediária pode ser ignorada. Porém, quando as conversões de tipo de dados falharem, você verá mensagens de erro diferentes daquelas geradas na conversão do valor xs:string intermediário. Por exemplo, se o método de valor não convertesse o valor `int` 100000 em `smallint`, a mensagem de erro anterior seria:  
  
 `The conversion of the nvarchar value '100000' overflowed an INT2 column. Use a larger integer column.`  
  
 No [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], sem a conversão intermediária em xs:string, a mensagem de erro é:  
  
 `Arithmetic overflow error converting expression to data type smallint.`  
  
### <a name="sqlcmdexe-behavior-change-in-xml-mode"></a>Alteração de comportamento de sqlcmd.exe no modo XML  
 Há alterações de comportamento, se você usar sqlcmd.exe com modo XML (: comando XML ON) ao executar SELECT * de T FOR XML...  
  
### <a name="dbcc-checkident-revised-message"></a>Mensagem DBCC CHECKIDENT revisada  
 Na [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], a mensagem retornada pelo comando DBCC CHECKIDENT mudou somente quando ele é usado com RESEED *new_reseed_value* para alterar o valor de identidade atual. A nova mensagem é "Verificando informações de identidade: valor de identidade atual '\<valor de identidade atual >'. A execução do DBCC foi concluída. Se o DBCC imprimiu mensagens de erro, entre em contato com o administrador do sistema".  
  
 Em versões anteriores, a mensagem é "Verificando informações de identidade: valor de identidade atual '\<valor de identidade atual >', valor de coluna atual '\<valor atual da coluna >'. A execução do DBCC foi concluída. Se o DBCC imprimiu mensagens de erro, entre em contato com o administrador do sistema". A mensagem não muda quando DBCC CHECKIDENT é especificado com NORESEED, sem um segundo parâmetro ou sem um valor reseed. Para obter mais informações, veja [DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql).  
  
### <a name="behavior-of-exist-function-on-xml-datatype-has-changed"></a>O comportamento da função exist() no tipo de dados XML mudou  
 O comportamento do **exist ()** função mudou em comparação a um tipo de dados XML com um valor nulo para 0 (zero). Considere o exemplo a seguir:  
  
```xml  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 0;  
```  
  
 Nas versões anteriores, esta comparação retorna 1 (true); agora, esta comparação retorna 0 (zero, false).  
  
 As comparações a seguir não mudaram:  
  
```xml  
DECLARE @test XML;  
SET @test = null;  
SELECT COUNT(1) WHERE @test.exist('/dogs') = 1; -- 0 expected, 0 returned  
SELECT COUNT(1) WHERE @test.exist('/dogs') IS NULL; -- 1 expected, 1 returned  
```  
  
## <a name="see-also"></a>Consulte também  
 [Alterações recentes em recursos do mecanismo de banco de dados no SQL Server 2014](breaking-changes-to-database-engine-features-in-sql-server-2016.md)   
 [Recursos do mecanismo de banco de dados preteridos no SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md)   
 [Funcionalidade do mecanismo de banco de dados descontinuada no SQL Server 2014](discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
