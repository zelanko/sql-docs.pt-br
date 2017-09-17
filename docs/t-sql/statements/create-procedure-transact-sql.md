---
title: Criar procedimento (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PROC
- PROCEDURE
- CREATE PROCEDURE
- CREATE_PROC_TSQL
- PROCEDURE_TSQL
- CREATE PROC
- PROC_TSQL
- CREATE_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- table-valued parameters
- SET statement, stored procedures
- stored procedures [SQL Server], creating
- wildcard parameters [SQL Server]
- maximum size of stored procedures
- WITH RECOMPILE clause
- common language runtime [SQL Server], stored procedures
- CREATE PROCEDURE statement
- local temporary procedures [SQL Server]
- WITH ENCRYPTION clause
- output parameters [SQL Server]
- nesting stored procedures
- user-defined stored procedures [SQL Server]
- system stored procedures [SQL Server], creating
- deferred name resolution, stored procedures
- referenced tables [SQL Server]
- global temporary procedures [SQL Server]
- cursor data type
- temporary stored procedures [SQL Server]
- size [SQL Server], stored procedures
- automatic stored procedure execution
- creating stored procedures
ms.assetid: afe3d86d-c9ab-44e4-b74d-4e3dbd9cc58c
caps.latest.revision: 180
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: c2a0a43aefe59bc11f16445b5ee0c781179a33fa
ms.openlocfilehash: 23460288040b37ec6a09293bc02a46e4f9af94fa
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="create-procedure-transact-sql"></a>CREATE PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cria um [!INCLUDE[tsql](../../includes/tsql-md.md)] ou common language runtime (CLR) armazenado procedimento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], Azure SQL Data Warehouse e o Parallel Data Warehouse. Procedimentos armazenados são semelhantes a procedimentos em outras linguagens de programação no sentido de que podem:  
  
-   Aceitar parâmetros de entrada e retornar vários valores no formulário de parâmetros de saída para o procedimento de chamada ou lote.  
  
-   Conter instruções de programação que executam operações no banco de dados, inclusive chamar outros procedimentos.  
  
-   Retornar um valor de status a um procedimento de chamada ou lote para indicar êxito ou falha (e o motivo da falha).  
  
 Use esta instrução para criar um procedimento permanente no banco de dados atual ou um procedimento temporário no **tempdb** banco de dados.  
  
> [!NOTE]  
>  A integração do CLR do .NET Framework para SQL Server é discutida neste tópico. Integração CLR não se aplicam ao Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

Ir para [exemplos simples](#Simple) ignorar os detalhes da sintaxe e obter um exemplo rápido de básico de procedimento armazenado.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Transact-SQL Syntax for Stored Procedures in SQL Server and Azure SQL Database  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } 
    [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }  
        [ VARYING ] [ = default ] [ OUT | OUTPUT | [READONLY]  
    ] [ ,...n ]   
[ WITH <procedure_option> [ ,...n ] ]  
[ FOR REPLICATION ]   
AS { [ BEGIN ] sql_statement [;] [ ...n ] [ END ] }  
[;]  
  
<procedure_option> ::=   
    [ ENCRYPTION ]  
    [ RECOMPILE ]  
    [ EXECUTE AS Clause ]  
```  
  
```  
-- Transact-SQL Syntax for CLR Stored Procedures  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } 
    [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH EXECUTE AS Clause ]  
AS { EXTERNAL NAME assembly_name.class_name.method_name }  
[;]  
```  
  
```  
-- Transact-SQL Syntax for Natively Compiled Stored Procedures  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } [schema_name.] procedure_name  
    [ { @parameter data_type } [ NULL | NOT NULL ] [ = default ] 
        [ OUT | OUTPUT ] [READONLY] 
    ] [ ,... n ]  
  WITH NATIVE_COMPILATION, SCHEMABINDING [ , EXECUTE AS clause ]  
AS  
{  
  BEGIN ATOMIC WITH (set_option [ ,... n ] )  
sql_statement [;] [ ... n ]  
 [ END ]  
}  
 [;]  
  
<set_option> ::=  
    LANGUAGE =  [ N ] 'language'  
  | TRANSACTION ISOLATION LEVEL =  { SNAPSHOT | REPEATABLE READ | SERIALIZABLE }  
  | [ DATEFIRST = number ]  
  | [ DATEFORMAT = format ]  
  | [ DELAYED_DURABILITY = { OFF | ON } ]  
```  
  
```  
-- Transact-SQL Syntax for Stored Procedures in Azure SQL Data Warehouse
-- and Parallel Data Warehouse  
  
-- Create a stored procedure   
CREATE { PROC | PROCEDURE } [ schema_name.] procedure_name  
    [ { @parameterdata_type } [ OUT | OUTPUT ] ] [ ,...n ]  
AS { [ BEGIN ] sql_statement [;][ ,...n ] [ END ] }  
[;]  
```  
  
## <a name="arguments"></a>Argumentos
OU ALTER  
 **Aplica-se a**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (começando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).  
  
 Altera o procedimento se ele já existe.
 
 *schema_name*  
 O nome do esquema ao qual o procedimento pertence. Os procedimentos são associados a esquemas. Se não for especificado um nome de esquema quando o procedimento é criado, será atribuído automaticamente o esquema padrão do usuário que estiver criando o procedimento.  
  
 *procedure_name*  
 O nome do procedimento. Nomes de procedimento devem estar de acordo com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md) e deve ser exclusivo dentro do esquema.  
  
 Evite usar o **SP _** prefixo ao nomear procedimentos. Esse prefixo é usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para designar procedimentos de sistema. O uso do prefixo poderá causar a quebra do código do aplicativo se houver um procedimento de sistema com o mesmo nome.  
  
 Procedimentos temporários locais ou globais podem ser criados usando um sinal numérico (#) antes de *procedure_name* (*procedure_name #*) para os procedimentos temporários locais e dois sinais numéricos para temporário global procedimentos (*procedure_name #*). Um procedimento temporário local é visível somente à conexão que o criou e é descartado quando essa conexão é fechada. Um procedimento temporário global fica disponível para todas as conexões e é descartado ao término da última sessão que usa o procedimento. Nomes temporários não podem ser especificados para procedimentos CLR.  
  
 O nome completo de um procedimento ou um procedimento temporário global, incluindo ##, não pode exceder 128 caracteres. O nome completo de um procedimento temporário local, incluindo #, não pode exceder 116 caracteres.  
  
 **;**  *número*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Um inteiro opcional usado para agrupar procedimentos do mesmo nome. Esses procedimentos agrupados podem ser descartados juntos com o uso de uma instrução DROP PROCEDURE.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Procedimentos numerados não é possível usar o **xml** ou tipos de CLR definido pelo usuário e não pode ser usado em um guia de plano.  
  
 **@***parâmetro*  
 Um parâmetro declarado no procedimento. Especifique um nome de parâmetro usando o sinal de arroba (**@**) como o primeiro caractere. O nome do parâmetro deve estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md). Os parâmetros são locais para o procedimento; os mesmos nomes de parâmetro podem ser usados em outros procedimentos.  
  
 Podem ser declarados um ou mais parâmetros; o número máximo é 2.100. O valor de cada parâmetro declarado deve ser fornecido pelo usuário quando o procedimento é chamado, a menos que um valor padrão para o parâmetro seja especificado ou o valor seja definido como igual a outro parâmetro. Se o procedimento contiver [parâmetros com valor de tabela](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)e o parâmetro ausente na chamada, uma tabela vazia é transmitida. Os parâmetros podem assumir apenas o lugar de expressões constantes. Eles não podem ser usados no lugar de nomes de tabela, nomes de coluna ou nomes de outros objetos de banco de dados. Para obter mais informações, veja [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
 Os parâmetros não poderão ser declarados se FOR REPLICATION for especificado.  
  
 [ *type_schema_name***.** ] *data_type*  
 O tipo de dados do parâmetro e o esquema ao qual o tipo de dados pertence.  
  
**Diretrizes para [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos**:  
  
-   Todos os [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de dados podem ser usados como parâmetros.  
  
-   Você pode usar o tipo de tabela definido pelo usuário para criar parâmetros com valor de tabela. Os parâmetros com valor de tabela podem ser apenas parâmetros INPUT e devem ser acompanhados pela palavra-chave READONLY. Para obter mais informações, consulte [usar parâmetros &#40; mecanismo de banco de dados &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
  
-   **cursor** tipos de dados podem ser apenas parâmetros de saída e devem ser acompanhados pela palavra-chave VARYING.  
  
**Diretrizes para procedimentos CLR**:  
  
-   Todos os tipos de dados nativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tenham um equivalente em código gerenciado podem ser usados como parâmetros. Para obter mais informações sobre a correspondência entre tipos CLR e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados do sistema, consulte [mapeamento de dados de parâmetro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md). Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados do sistema e sua sintaxe, consulte [tipos de dados &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md).  
  
-   Com valor de tabela ou **cursor** tipos de dados não podem ser usados como parâmetros.  
  
-   Se o tipo de dados do parâmetro for um tipo de dados CLR definido pelo usuário, será necessário ter a permissão EXECUTE para o tipo.  
  
VARYING  
 Especifica o conjunto de resultados com suporte como um parâmetro de saída. Este parâmetro é construído dinamicamente pelo procedimento e seu conteúdo pode variar. Aplica-se somente a **cursor** parâmetros. Esta opção não é válida para procedimentos CLR.  
  
*padrão*  
 Um valor padrão para um parâmetro. Se um valor padrão é definido para um parâmetro, o procedimento pode ser executado sem especificar um valor para esse parâmetro. O valor padrão deve ser uma constante ou pode ser NULL. O valor constante pode estar na forma de um curinga, tornando possível usar a palavra-chave LIKE ao passar o parâmetro para o procedimento.   
  
 Valores padrão são registrados no **sys.parameters.default** coluna somente para procedimentos CLR. Essa coluna é NULL para [!INCLUDE[tsql](../../includes/tsql-md.md)] parâmetros de procedimento.  
  
OUT | OUTPUT  
 Indica que o parâmetro é um parâmetro de saída. Use parâmetros OUTPUT para retornar valores ao chamador do procedimento. **texto**, **ntext**, e **imagem** parâmetros não podem ser usados como parâmetros de saída, a menos que o procedimento seja CLR. Um parâmetro de saída pode ser um espaço reservado de cursor, a menos que o procedimento seja CLR. Um tipo de dados com valor de tabela não pode ser especificado como um parâmetro OUTPUT de um procedimento.  
  
READONLY  
 Indica que o parâmetro não pode ser atualizado ou modificado no corpo do procedimento. Se o tipo de parâmetro for um tipo com valor de tabela, deverá ser especificado READONLY.  
  
RECOMPILE  
 Indica que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não armazena em cache um plano de consulta para esse procedimento, forçando-o a ser compilados cada vez que ele é executado. Para obter mais informações sobre os motivos para forçar uma recompilação, consulte [recompilar um procedimento armazenado](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md). Esta opção não pode ser usada quando FOR REPLICATION é especificado ou para procedimentos CLR.  
  
 Para instruir o [!INCLUDE[ssDE](../../includes/ssde-md.md)] a descartar planos de consulta para consultas individuais dentro de um procedimento, use a dica de consulta RECOMPILE na definição da consulta. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
ENCRYPTION  
 **Aplica-se a**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte o texto original da instrução CREATE PROCEDURE em um formato ofuscado. A saída do ofuscamento não é diretamente visível em quaisquer exibições de catálogo no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os usuários que não tiverem nenhum acesso a tabelas do sistema ou arquivos de banco de dados não poderão recuperar o texto ofuscado. No entanto, o texto está disponível para usuários privilegiados que puderem acessar as tabelas do sistema sobre a [porta DAC](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) ou acessar diretamente os arquivos de banco de dados. Além disso, os usuários que podem anexar um depurador ao processo de servidor também podem recuperar o procedimento descriptografado da memória em tempo de execução. Para obter mais informações sobre como acessar metadados do sistema, consulte [configuração de visibilidade de metadados](../../relational-databases/security/metadata-visibility-configuration.md).  
  
 Esta opção não é válida para procedimentos CLR.  
  
 Procedimentos criados com esta opção não podem ser publicados como parte de replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
EXECUTE AS *cláusula*  
 Especifica o contexto de segurança no qual o procedimento deve ser executado.  
  
 Para procedimentos armazenados compilados nativamente, iniciando [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], há nenhuma limitação em EXECUTE AS cláusula. Em [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SELF, OWNER e *'user_name'* cláusulas têm suporte com procedimentos armazenados compilados nativamente.  
  
 Para obter mais informações, veja [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
FOR REPLICATION  
 **Aplica-se a**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica que o procedimento é criado para replicação. Consequentemente, não pode ser executado no Assinante. Um procedimento criado com a opção FOR REPLICATION é usado como um filtro de procedimento e é executado somente durante a replicação. Os parâmetros não poderão ser declarados se FOR REPLICATION for especificado. FOR REPLICATION não pode ser especificado para procedimentos CLR. A opção RECOMPILE é ignorada para procedimentos criados com FOR REPLICATION.  
  
 Um `FOR REPLICATION` procedimento tem um tipo de objeto **RF** na **sys. Objects** e **Procedures**.  
  
 {[BEGIN] *sql_statement* [;] [ ...  *n*  ] [END]}  
 Uma ou mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] que abrangem o corpo do procedimento. Você pode usar as palavras-chave BEGIN e END para delimitar as instruções. Para obter informações, consulte as seções Práticas recomendadas, Comentários gerais e Limitações e restrições a seguir.  
  
NOME externo *nome_do_assembly***.** *class_name***.** *nome_do_método*  
 **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica o método de um assembly [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para um procedimento CLR a ser referenciado. *class_name* deve ser um válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador e deve existir como uma classe no assembly. Se a classe tiver um nome qualificado de namespace que usa um período (**.**) para separar partes do namespace, o nome da classe deve ser delimitado usando colchetes (**[]**) ou aspas (**""**). O método especificado deve ser um método estático da classe.  
  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode executar código CLR. Você pode criar, modificar e descartar objetos do banco de dados que fazem referência a módulos CLR; No entanto, você não pode executar essas referências no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] até que você habilite o [opção clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Para habilitar a opção, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Não há suporte para procedimentos CLR em um banco de dados independente.  
  
ATOMIC WITH  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica a execução atômica de procedimento armazenado. As alterações são confirmadas ou todas as alterações são revertidas pelo lançamento de uma exceção. O bloco ATOMIC WITH é necessário para procedimentos armazenados compilados nativamente.  
  
 Se o procedimento for retornado (explicitamente por meio da instrução RETURN ou implicitamente para concluir a execução), o trabalho executado pelo procedimento será confirmado. Se o procedimento for acionado (com a instrução THROW), o trabalho executado pelo procedimento será revertido.  
  
 XACT_ABORT está ON por padrão em um bloco atômico e não pode ser alterado. XACT_ABORT especifica se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reverte automaticamente a transação atual quando uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] gera um erro em tempo de execução.  
  
 As seguintes opções SET estão sempre ON; no bloco ATOMIC as opções não podem ser alteradas.  
-   CONCAT_NULL_YIELDS_NULL  
-   QUOTED_IDENTIFIER, ARITHABORT  
-   NOCOUNT  
-   ANSI_NULLS  
-   ANSI_WARNINGS  
  
As opções SET não podem ser alteradas nos blocos ATOMIC. As opções SET na sessão de usuário não são usadas no escopo dos procedimentos armazenados compilados nativamente. Essas opções são fixas no tempo de compilação.  
  
As operações BEGIN, ROLLBACK e COMMIT não podem ser usadas dentro de um bloco atômico.  
  
 Há um bloco ATOMIC por procedimento armazenado originalmente compilado, no escopo exterior do procedimento. Os blocos não podem ser aninhados. Para obter mais informações sobre blocos atômicos, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
**NULO** | NÃO NULO  
 Determina se são permitidos valores nulos em um parâmetro. NULL é o padrão.  
  
NATIVE_COMPILATION  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica que o procedimento foi originalmente compilado. NATIVE_COMPILATION, SCHEMABINDING e EXECUTE AS podem ser especificados em qualquer ordem. Para obter mais informações, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
SCHEMABINDING  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Assegura que as tabelas que são referenciadas por um procedimento não possam ser descartadas ou alteradas. SCHEMABINDING é necessário em procedimentos armazenados compilados nativamente. (Para obter mais informações, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).) As restrições SCHEMABINDING são as mesmas para funções definidas pelo usuário. Para obter mais informações, consulte a seção SCHEMABINDING [CREATE FUNCTION &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md).  
  
LANGUAGE = [N] 'language'  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Equivalente a [Definir idioma &#40; Transact-SQL &#41; ](../../t-sql/statements/set-language-transact-sql.md) opção de sessão. LANGUAGE = [N] 'language' é obrigatório.  
  
TRANSACTION ISOLATION LEVEL  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Exigido para procedimentos armazenados compilados nativamente. Especifica o nível de isolamento da transação para o procedimento armazenado. As opções são as seguintes:  
  
 Para obter mais informações sobre essas opções, consulte [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
REPEATABLE READ  
 Especifica que as instruções não podem ler dados que foram modificados, mas ainda não foram confirmados por outras transações. Se outra transação modifica os dados que foram lidos pela transação atual, a transação atual falhará.  
  
SERIALIZABLE  
 Especifica o seguinte:  
-   As instruções não podem ler dados que foram modificados, mas que ainda não foram confirmados por outras transações.  
-   Se outras transações modificarem dados que foram lidos pela transação atual, a transação atual falhará.  
-   Se outra transação inserir linhas novas com valores chave que estejam no intervalo de chaves lido por qualquer instrução na transação atual, a transação atual falhará.  
  
SNAPSHOT  
 Especifica que os dados lidos por qualquer instrução em uma transação são a versão transacionalmente consistente dos dados que existiam no início da transação.  
  
DATEFIRST = *número*  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica o primeiro dia da semana como um número de 1 a 7. DATEFIRST é opcional. Se não for especificado, a configuração será inferida do idioma especificado.  
  
 Para obter mais informações, consulte [SET DATEFIRST &#40; Transact-SQL &#41; ](../../t-sql/statements/set-datefirst-transact-sql.md).  
  
DATEFORMAT = *formato*  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica a ordem das partes do mês, dia e ano para interpretar cadeias de caracteres date, smalldatetime, datetime, datetime2 e datetimeoffset. DATEFORMAT é opcional. Se não for especificado, a configuração será inferida do idioma especificado.  
  
 Para obter mais informações, consulte [SET DATEFORMAT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-dateformat-transact-sql.md).  
  
DELAYED_DURABILITY = { OFF | ON }  
 **Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as confirmações de transações podem ser completamente duráveis, o padrão, ou duráveis atrasadas.  
  
 Para obter mais informações, consulte [controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md).  

## <a name="Simple"></a>Exemplos simples

Para ajudá-lo a começar, aqui estão dois exemplos rápidos:  
`SELECT DB_NAME() AS ThisDB;`Retorna o nome do banco de dados atual.  
Você pode encapsular essa instrução em um procedimento armazenado, tais como:  
```sql  
CREATE PROC What_DB_is_this     
AS   
SELECT DB_NAME() AS ThisDB; 
```   
Chame o procedimento de armazenamento com a instrução:`EXEC What_DB_is_this;`   

Um pouco mais complexo, é fornecer um parâmetro de entrada para tornar o procedimento mais flexíveis. Por exemplo:  
```sql   
CREATE PROC What_DB_is_that @ID int   
AS    
SELECT DB_NAME(@ID) AS ThatDB;   
```   
Forneça um número de id do banco de dados quando você chamar o procedimento. Por exemplo, `EXEC What_DB_is_that 2;` retorna `tempdb`.   

Consulte [exemplos](#Examples) em direção ao final deste tópico para muitos outros exemplos.     
    
## <a name="best-practices"></a>Práticas recomendadas  
 Embora esta não seja uma lista completa de práticas recomendadas, estas sugestões podem melhorar o desempenho do procedimento.  
  
-   Use a instrução SET NOCOUNT ON como a primeira instrução no corpo do procedimento. Ou seja, coloque-a logo após a palavra-chave AS. Isso desativa as mensagens que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envia ao cliente após a execução de qualquer instrução SELECT, INSERT, UPDATE, MERGE e DELETE. O desempenho global do banco de dados e do aplicativo melhora ao eliminar essa sobrecarga de rede desnecessária. Para obter informações, consulte [SET NOCOUNT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-nocount-transact-sql.md).  
  
-   Use nomes de esquemas ao criar ou referenciar objetos de banco de dados no procedimento. Leva menos tempo de processamento o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para resolver os nomes de objeto se ele tem que pesquisar vários esquemas. Ele também evita problemas de acesso causados pelo esquema padrão de um usuário que está sendo atribuída quando objetos são criados sem especificar o esquema e permissão.  
  
-   Evite ajustar funções ao redor de colunas especificadas nas cláusulas WHERE e JOIN. Isso torna as colunas não determinísticas e impede o processador de consultas de usar índices.  
  
-   Evite usar funções escalares em instruções SELECT que retornam muitas linhas de dados. Como a função escalar deve ser se aplicada a cada linha, o comportamento resultante é como o processamento baseado em linha e afeta o desempenho.  
  
-   Evite o uso de `SELECT *`. Em vez disso, especifique os nomes de colunas necessários. Isso pode evitar alguns erros do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que param a execução do procedimento. Por exemplo, um `SELECT *` instrução que retorna dados de uma tabela de 12 colunas e, em seguida, insere dados em uma tabela temporária de 12 colunas terá êxito até que o número ou a ordem das colunas de uma tabela é alterada.  
  
-   Evite processar ou retornar dados em excesso. Delimite os resultados o quanto antes no código do procedimento, para que quaisquer operações subsequentes executadas pelo procedimento sejam efetuadas com o menor conjunto de dados possível. Envie apenas os dados essenciais ao aplicativo cliente. Além disso, enviar somente os dados essenciais ao aplicativo cliente é mais eficiente do que enviar dados adicionais pela rede e forçar o aplicativo cliente a trabalhar com conjuntos de resultados desnecessariamente grandes.  
  
-   Usar transações explícitas usando BEGIN/COMMIT TRANSACTION e mantenha as transações tão curtas quanto possível. Transações maiores indicam bloqueio de registro mais longo e um maior potencial para deadlock.  
  
-   Use o recurso TRY…CATCH do [!INCLUDE[tsql](../../includes/tsql-md.md)] para tratamento de erros em um procedimento. TRY…CATCH pode encapsular um bloco inteiro de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Isso cria menos sobrecarga de desempenho e também torna o relatório de erros mais preciso com muito menos programação.  
  
-   Use a palavra-chave DEFAULT em todas as colunas de tabela que sejam referenciadas pelas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE ou ALTER TABLE no corpo do procedimento. Isso impede que passar NULL para colunas que não permitem valores nulos.  
  
-   Use NULL ou NOT NULL para cada coluna em uma tabela temporária. As opções ANSI_DFLT_ON e ANSI_DFLT_OFF controlam a forma como o [!INCLUDE[ssDE](../../includes/ssde-md.md)] atribui os atributos NULL ou NOT NULL a colunas quando esses atributos não são especificados em uma instrução CREATE TABLE ou ALTER TABLE. Se uma conexão executar um procedimento com configurações para essas opções diferentes da conexão que criou o procedimento, as colunas da tabela criada para a segunda conexão poderão ter nulidades diferentes e exibir um comportamento diferente. Se NULL ou NOT NULL for declarado explicitamente para cada coluna, as tabelas temporárias serão criadas com a mesma nulidade para todas as conexões que executam o procedimento.  
  
-   Use instruções de modificação que convertam nulos e inclua uma lógica que elimine linhas com valores nulos das consultas. Lembre-se que em [!INCLUDE[tsql](../../includes/tsql-md.md)], NULL não está vazio ou "nada" de valor. É um espaço reservado para um valor desconhecido e pode causar um comportamento inesperado, especialmente ao consultar conjuntos de resultados ou usar funções AGGREGATE.  
  
-   Use o operador UNION ALL em vez dos operadores UNION ou OR, a menos que haja uma necessidade específica de valores distintos. O operador UNION ALL requer menos sobrecarga de processamento, pois as duplicatas não são filtradas do conjunto de resultados.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Não há um tamanho máximo predefinido para um procedimento.  
  
 Variáveis especificadas no procedimento podem ser definido pelo usuário ou variáveis do sistema, como @@SPID.  
  
 Quando um procedimento é executado pela primeira vez, ele é compilado para determinar um plano de acesso ideal para recuperar os dados. As execuções subsequentes do procedimento poderão reutilizar o plano já gerado se ele ainda estiver no cache de planos do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Um ou mais procedimentos podem ser executados automaticamente quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado. Os procedimentos devem ser criados pelo administrador do sistema no **mestre** de banco de dados e executado sob o **sysadmin** função fixa de servidor como um processo em segundo plano. Os procedimentos não podem ter nenhum parâmetro de entrada ou de saída. Para obter mais informações, consulte [executar um procedimento armazenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md).  
  
 Procedimentos são aninhados quando um procedimento chama outro ou executa código gerenciado, referenciando uma rotina, tipo ou agregação CLR. Os procedimentos e as referências de código gerenciado podem ser aninhados em até 32 níveis. O aninhamento fica um nível acima quando o procedimento chamado ou a referência de código gerenciado inicia sua execução e fica um nível abaixo quando a execução do procedimento chamado ou da referência de código gerenciado é concluída. Os métodos invocados do código gerenciado não contam em relação ao limite de níveis de aninhamento. Entretanto, quando um procedimento armazenado CLR executa operações de acesso de dados por meio do provedor gerenciado SQL Server, mais um nível de aninhamento é adicionado na transição de código gerenciado para SQL.  
  
 Tentar exceder o máximo de níveis de aninhamento causará a falha da cadeia de chamada inteira. Você pode usar o @@NESTLEVEL função para retornar o nível de aninhamento da execução do procedimento armazenado atual.  
  
## <a name="interoperability"></a>Interoperabilidade  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] salva as configurações de SET QUOTED_IDENTIFIER e SET ANSI_NULLS quando um procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)] é criado ou modificado. Essas configurações originais são usadas quando o procedimento é executado. Portanto, qualquer configuração de sessão de cliente para SET QUOTED_IDENTIFIER e SET ANSI_NULLS é ignorada quando o procedimento é executado.  
  
 Outras opções SET, tais como SET ARITHABORT, SET ANSI_WARNINGS ou SET ANSI_PADDINGS não são salvas quando um procedimento é criado ou modificado. Se a lógica do armazenado depender de uma configuração particular, inclua uma instrução SET no início do procedimento para assegurar a configuração apropriada. Quando uma instrução SET é executada a partir de um procedimento, a configuração permanece em vigor somente até o procedimento concluir a execução. A configuração é então restaurada no valor existente quando o procedimento foi chamado. Isso permite que clientes individuais definam as opções desejadas sem afetar a lógica do procedimento.  
  
 Qualquer instrução SET pode ser especificada dentro de um procedimento, exceto SET SHOWPLAN_TEXT e SET SHOWPLAN_ALL. Elas devem ser as únicas instruções no lote. A opção SET escolhida permanece em vigor durante a execução do procedimento e depois é revertida para sua configuração anterior.  
  
> [!NOTE]  
>  SET ANSI_WARNINGS não é cumprido ao passar parâmetros em um procedimento, em uma função definida pelo usuário ou ao declarar e definir variáveis em uma instrução de lote. Por exemplo, se a variável é definida como **char**(3) e definido como um valor maior do que três caracteres, os dados são truncados para o tamanho definido e a inserção ou atualização instrução tem sucesso.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 A instrução CREATE PROCEDURE não pode ser combinada com outras instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] em um único lote.  
  
 As instruções a seguir não podem ser usadas em qualquer lugar no corpo de um procedimento armazenado.  
  
||||  
|-|-|-|  
|CREATE AGGREGATE|CREATE SCHEMA|SET SHOWPLAN_TEXT|  
|CREATE DEFAULT|CREATE ou ALTER TRIGGER|SET SHOWPLAN_XML|  
|CREATE ou ALTER FUNCTION|CREATE ou ALTER VIEW|USE *database_name*|  
|CREATE ou ALTER PROCEDURE|SET PARSEONLY||  
|CREATE RULE|SET SHOWPLAN_ALL||  
  
 Um procedimento pode referenciar tabelas que ainda não existem. No momento da criação, apenas a verificação de sintaxe é executada. O procedimento não é compilado até ser executado pela primeira vez. Somente durante a compilação todos os objetos referenciados no procedimento são resolvidos. Portanto, um procedimento sintaticamente correto que referencia tabelas que não existem pode ser criado com êxito; No entanto, o procedimento falhará em tempo de execução se as tabelas referenciadas não existirem.  
  
 Você não pode especificar um nome de função como um valor padrão de parâmetro ou como o valor passado para um parâmetro durante a execução de um procedimento. Entretanto, você pode passar uma função como uma variável, conforme mostrado no seguinte exemplo:  
  
```  
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;   
GO  
```  
  
 Se o procedimento fizer modificações em uma instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], essas modificações não poderão ser revertidas. Procedimentos remotos não participam das transações.  
  
 Para que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] referencie o método correto quando estiver sobrecarregado no .NET Framework, o método especificado na cláusula EXTERNAL NAME deverá ter as seguintes características:  
  
-   Ser declarado como um método estático.  
  
-   Receber o mesmo número de parâmetros que o procedimento.  
  
-   Usar tipos de parâmetro que sejam compatíveis com os tipos de dados dos parâmetros correspondentes do procedimento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre a correspondência de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados para o [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipos de dados, consulte [mapeamento de dados de parâmetro CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
## <a name="metadata"></a>Metadados  
 A tabela a seguir lista as exibições do catálogo e as exibições de gerenciamento dinâmico que você pode usar para retornar informações sobre procedimentos armazenados.  
  
|Exibição|Description|  
|----------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|Retorna a definição de um procedimento [!INCLUDE[tsql](../../includes/tsql-md.md)]. O texto de um procedimento criado com a opção de criptografia não pode ser exibido usando o **sql_modules** exibição do catálogo.|  
|[assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|Retorna informações sobre um procedimento CLR.|  
|[sys. Parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|Retorna informações sobre os parâmetros que são definidos em um procedimento.|  
|[sys. sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) [sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) [sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)|Retorna os objetos referenciados por um procedimento.|  
  
 Para calcular o tamanho de um procedimento compilado, use os Contadores de Desempenho do Sistema a seguir.  
  
|Nome de objeto do Monitor de Desempenho|Nome do Contador de Desempenho do Sistema|  
|-------------------------------------|--------------------------------------|  
|Objeto SQLServer: cache de planos|Taxa de Acertos do Cache|  
||Páginas do Cache|  
||Contagens de Objetos do Cache*|  
  
 *Esses contadores estão disponíveis para várias categorias de objetos de cache, inclusive [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, [!INCLUDE[tsql](../../includes/tsql-md.md)] preparado, procedimentos, gatilhos e outros. Para obter mais informações, consulte [do SQL Server, objeto de Cache de plano](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer **CREATE PROCEDURE** no banco de dados e **ALTER** permissão no esquema no qual o procedimento está sendo criado ou requer a participação no **db_ddladmin** função fixa de banco de dados.  
  
 Para procedimentos armazenados CLR, requer a propriedade do assembly referenciado na cláusula EXTERNAL NAME, ou **referências** permissão nesse assembly.  
  
##  <a name="mot"></a>CREATE PROCEDURE e tabelas com otimização de memória  
 Tabelas com otimização de memória podem ser acessadas por meio de procedimentos armazenados tradicionais e compilados nativamente. Procedimentos nativos são na maioria dos casos, a maneira mais eficiente.
Para obter mais informações, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
 O exemplo a seguir mostra como criar um procedimento armazenado compilado nativamente que acessa uma tabela com otimização de memória `dbo.Departments`:  
  
```sql  
CREATE PROCEDURE dbo.usp_add_kitchen @dept_id int, @kitchen_count int NOT NULL  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  
  UPDATE dbo.Departments  
  SET kitchen_count = ISNULL(kitchen_count, 0) + @kitchen_count  
  WHERE id = @dept_id  
END;  
GO  
```  
  
 Um procedimento criado sem o NATIVE_COMPILATION não pode ser alterado para um procedimento armazenado originalmente compilado. 
  
 Para obter uma discussão sobre programação em procedimentos armazenados compilados nativamente, suporte a área de superfície de consulta e operadores, consulte [recursos com suporte para compilados nativamente módulos T-SQL](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
## <a name="Examples"></a> Exemplos  
  
|Categoria|Elementos de sintaxe em destaque|  
|--------------|------------------------------|  
|[Sintaxe básica](#BasicSyntax)|CREATE PROCEDURE|  
|[Passando parâmetros](#Parameters)|@parameter <br> &nbsp;&nbsp;• = default <br> &nbsp;&nbsp;• SAÍDA <br> &nbsp;&nbsp;tipo de parâmetro com valor de tabela • <br> &nbsp;&nbsp;• CURSOR VARYING|  
|[Modificando dados usando um procedimento armazenado](#Modify)|UPDATE|  
|[Tratamento de erros](#Error)|TRY…CATCH|  
|[Ofuscando a definição do procedimento](#Encrypt)|WITH ENCRYPTION|  
|[Forçar o recompilação do procedimento](#Recompile)|WITH RECOMPILE|  
|[Definir o contexto de segurança](#Security)|EXECUTE AS|  
  
###  <a name="BasicSyntax"></a>Sintaxe básica  
 Os exemplos desta seção demonstram a funcionalidade básica da instrução CREATE PROCEDURE por meio da sintaxe mínima necessária.  
  
#### <a name="a-creating-a-simple-transact-sql-procedure"></a>A. Criando um procedimento Transact-SQL simples  
 O exemplo a seguir cria um procedimento armazenado que retorna todos os funcionários (com os nomes e sobrenomes fornecidos), os cargos e os nomes de departamento em uma exibição no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Esse procedimento não usa nenhum parâmetro. O exemplo demonstra três métodos para executar o procedimento.  
  
```sql  
CREATE PROCEDURE HumanResources.uspGetAllEmployees  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment;  
GO  
  
SELECT * FROM HumanResources.vEmployeeDepartment;  
```  
  
 O `uspGetEmployees` procedimento pode ser executado das seguintes maneiras:  
  
```sql  
EXECUTE HumanResources.uspGetAllEmployees;  
GO  
-- Or  
EXEC HumanResources.uspGetAllEmployees;  
GO  
-- Or, if this procedure is the first statement within a batch:  
HumanResources.uspGetAllEmployees;  
```  
  
#### <a name="b-returning-more-than-one-result-set"></a>B. Retornando mais de um conjunto de resultados  
 O procedimento a seguir retorna dois conjuntos de resultados.  
  
```sql  
CREATE PROCEDURE dbo.uspMultipleResults   
AS  
SELECT TOP(10) BusinessEntityID, Lastname, FirstName FROM Person.Person;  
SELECT TOP(10) CustomerID, AccountNumber FROM Sales.Customer;  
GO  
```  
  
#### <a name="c-creating-a-clr-stored-procedure"></a>C. Criando um procedimento armazenado CLR  
 O exemplo a seguir cria o `GetPhotoFromDB` procedimento que referencia o `GetPhotoFromDB` método do `LargeObjectBinary` classe no `HandlingLOBUsingCLR` assembly. Antes do procedimento é criado, o `HandlingLOBUsingCLR` assembly é registrado no banco de dados local.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] (se usar um assembly criado a partir de *assembly_bits.*  
  
```sql  
CREATE ASSEMBLY HandlingLOBUsingCLR  
FROM '\\MachineName\HandlingLOBUsingCLR\bin\Debug\HandlingLOBUsingCLR.dll';  
GO  
CREATE PROCEDURE dbo.GetPhotoFromDB  
(  
    @ProductPhotoID int,  
    @CurrentDirectory nvarchar(1024),  
    @FileName nvarchar(1024)  
)  
AS EXTERNAL NAME HandlingLOBUsingCLR.LargeObjectBinary.GetPhotoFromDB;  
GO  
```  
  
###  <a name="Parameters"></a>Passando parâmetros  
 Os exemplos desta seção demonstram como usar parâmetros de entrada e saída para passar valores de e para um procedimento armazenado.  
  
#### <a name="d-creating-a-procedure-with-input-parameters"></a>D. Criando um procedimento com parâmetros de entrada  
 O exemplo a seguir cria um procedimento armazenado que retorna informações de um funcionário específico passando valores do nome e sobrenome do funcionário. Este procedimento aceita apenas correspondências exatas para os parâmetros passados.  
  
```sql  
IF OBJECT_ID ( 'HumanResources.uspGetEmployees', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetEmployees;  
GO  
CREATE PROCEDURE HumanResources.uspGetEmployees   
    @LastName nvarchar(50),   
    @FirstName nvarchar(50)   
AS   
  
    SET NOCOUNT ON;  
    SELECT FirstName, LastName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment  
    WHERE FirstName = @FirstName AND LastName = @LastName;  
GO  
  
```  
  
 O `uspGetEmployees` procedimento pode ser executado das seguintes maneiras:  
  
```  
EXECUTE HumanResources.uspGetEmployees N'Ackerman', N'Pilar';  
-- Or  
EXEC HumanResources.uspGetEmployees @LastName = N'Ackerman', @FirstName = N'Pilar';  
GO  
-- Or  
EXECUTE HumanResources.uspGetEmployees @FirstName = N'Pilar', @LastName = N'Ackerman';  
GO  
-- Or, if this procedure is the first statement within a batch:  
HumanResources.uspGetEmployees N'Ackerman', N'Pilar';  
  
```  
  
#### <a name="e-using-a-procedure-with-wildcard-parameters"></a>E. Usando um procedimento com parâmetros curinga  
 O exemplo a seguir cria um procedimento armazenado que retorna informações de funcionários passando valores totais ou parciais do nome e sobrenome do funcionário. Padrão deste procedimento corresponde aos parâmetros passados ou, se não for fornecido, usa o padrão predefinido (sobrenomes que começam com a letra `D`).  
  
```sql  
IF OBJECT_ID ( 'HumanResources.uspGetEmployees2', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetEmployees2;  
GO  
CREATE PROCEDURE HumanResources.uspGetEmployees2   
    @LastName nvarchar(50) = N'D%',   
    @FirstName nvarchar(50) = N'%'  
AS   
    SET NOCOUNT ON;  
    SELECT FirstName, LastName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment  
    WHERE FirstName LIKE @FirstName AND LastName LIKE @LastName;  
```  
  
 O `uspGetEmployees2` procedimento pode ser executado em muitas combinações. Apenas algumas combinações possíveis são mostradas aqui.  
  
```sql  
EXECUTE HumanResources.uspGetEmployees2;  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'Wi%';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 @FirstName = N'%';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'[CK]ars[OE]n';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'Hesse', N'Stefen';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'H%', N'S%';  
```  
  
#### <a name="f-using-output-parameters"></a>F. Usando parâmetros OUTPUT  
 O exemplo a seguir cria o procedimento `uspGetList`. Estes procedimentos retornam uma lista de produtos com preços que não excedem uma quantia especificada. O exemplo mostra o uso de várias instruções `SELECT` e vários parâmetros `OUTPUT`. Os parâmetros OUTPUT permitem que um procedimento externo, um lote ou mais de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] acessem um conjunto de valores durante a execução do procedimento.  
  
```sql  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
```  
  
 Execute `uspGetList` para retornar uma lista de produtos (bicicletas) da [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] que custam menos que `$700`. O `OUTPUT` parâmetros `@Cost` e `@ComparePrices` são usados com linguagem de controle de fluxo para retornar uma mensagem no **mensagens** janela.  
  
> [!NOTE]  
>  A variável OUTPUT deve ser definida quando o procedimento é criado e também quando a variável é usada. O nome do parâmetro e o nome da variável não precisa corresponder; No entanto, o tipo de dados e o posicionamento do parâmetro devem corresponder, a menos que `@ListPrice`  =  *variável* é usado.  
  
```sql  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
```  
  
 Este é o conjunto de resultados parcial:  
  
 ```   
 Product                     List Price  
 --------------------------  ----------  
 Road-750 Black, 58          539.99  
 Mountain-500 Silver, 40     564.99  
 Mountain-500 Silver, 42     564.99  
 ...  
 Road-750 Black, 48          539.99  
 Road-750 Black, 52          539.99  
   
 (14 row(s) affected)   
  
 These items can be purchased for less than $700.00.
 ```  
  
#### <a name="g-using-a-table-valued-parameter"></a>G. Usando um parâmetro com valor de tabela  
 O exemplo a seguir usa um tipo de parâmetro com valor de tabela para inserir várias linhas em uma tabela. O exemplo cria o tipo de parâmetro, declara uma variável de tabela para referenciá-lo, preenche a lista de parâmetros e passa os valores para um procedimento armazenado. O procedimento armazenado usa os valores para inserir várias linhas em uma tabela.  
  
```sql  
/* Create a table type. */  
CREATE TYPE LocationTableType AS TABLE   
( LocationName VARCHAR(50)  
, CostRate INT );  
GO  
  
/* Create a procedure to receive data for the table-valued parameter. */  
CREATE PROCEDURE usp_InsertProductionLocation  
    @TVP LocationTableType READONLY  
    AS   
    SET NOCOUNT ON  
    INSERT INTO [AdventureWorks2012].[Production].[Location]  
           ([Name]  
           ,[CostRate]  
           ,[Availability]  
           ,[ModifiedDate])  
        SELECT *, 0, GETDATE()  
        FROM  @TVP;  
GO  
  
/* Declare a variable that references the type. */  
DECLARE @LocationTVP   
AS LocationTableType;  
  
/* Add data to the table variable. */  
INSERT INTO @LocationTVP (LocationName, CostRate)  
    SELECT [Name], 0.00  
    FROM   
    [AdventureWorks2012].[Person].[StateProvince];  
  
/* Pass the table variable data to a stored procedure. */  
EXEC usp_InsertProductionLocation @LocationTVP;  
GO  
```  
  
##### <a name="h-using-an-output-cursor-parameter"></a>H. Usando um parâmetro de cursor OUTPUT  
 O exemplo a seguir usa o parâmetro de cursor OUTPUT para retornar um cursor local de um procedimento para o lote de chamada, procedimento ou gatilho.  
  
 Primeiro, crie o procedimento que declara e abre um cursor na tabela `Currency`:  
  
```sql  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
```  
  
 Em seguida, execute um lote que declare uma variável de cursor local, execute o procedimento para atribuir o cursor à variável local e depois busque as linhas do cursor.  
  
```sql  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
```  
  
###  <a name="Modify"></a>Modificando dados usando um procedimento armazenado  
 Os exemplos nesta seção demonstram como inserir ou modificar dados em tabelas ou exibições através da inclusão de uma instrução DML (linguagem de manipulação de dados) na definição do procedimento.  
  
#### <a name="i-using-update-in-a-stored-procedure"></a>I. Usando UPDATE em um procedimento armazenado  
 O seguinte exemplo usa uma instrução UPDATE em um procedimento armazenado: o procedimento utiliza um parâmetro de entrada, `@NewHours`, e um parâmetro de saída, `@RowCount`. O `@NewHours` o valor do parâmetro é usado na instrução UPDATE para atualizar a coluna `VacationHours` na tabela `HumanResources.Employee`. O parâmetro de saída `@RowCount` é usado para retornar o número de linhas afetadas para uma variável local. Um expressão CASE é usada na cláusula SET para determinar condicionalmente o valor definido para `VacationHours`. Quando o funcionário é pago por hora (`SalariedFlag` = 0), `VacationHours` é definido como o número atual de horas mais o valor especificado em `@NewHours`; caso contrário, `VacationHours` é definido como o valor especificado em `@NewHours`.  
  
```sql  
CREATE PROCEDURE HumanResources.Update_VacationHours  
@NewHours smallint  
AS   
SET NOCOUNT ON;  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN SalariedFlag = 0 THEN VacationHours + @NewHours  
         ELSE @NewHours  
       END  
    )  
WHERE CurrentFlag = 1;  
GO  
  
EXEC HumanResources.Update_VacationHours 40;  
```  
  
###  <a name="Error"></a>Tratamento de erros  
 Os exemplos desta seção demonstram métodos para tratar erros que podem ocorrer durante a execução do procedimento armazenado.  
  
#### <a name="j-using-trycatch"></a>J. Usando TRY…CATCH  
 O exemplo a seguir usa a construção TRY…CATCH para retornar informações de erros obtidos durante a execução de um procedimento armazenado.  
  
```sql  
CREATE PROCEDURE Production.uspDeleteWorkOrder ( @WorkOrderID int )  
AS  
SET NOCOUNT ON;  
BEGIN TRY  
   BEGIN TRANSACTION   
   -- Delete rows from the child table, WorkOrderRouting, for the specified work order.  
   DELETE FROM Production.WorkOrderRouting  
   WHERE WorkOrderID = @WorkOrderID;  
  
   -- Delete the rows from the parent table, WorkOrder, for the specified work order.  
   DELETE FROM Production.WorkOrder  
   WHERE WorkOrderID = @WorkOrderID;  
  
   COMMIT  
  
END TRY  
BEGIN CATCH  
  -- Determine if an error occurred.  
  IF @@TRANCOUNT > 0  
     ROLLBACK  
  
  -- Return the error information.  
  DECLARE @ErrorMessage nvarchar(4000),  @ErrorSeverity int;  
  SELECT @ErrorMessage = ERROR_MESSAGE(),@ErrorSeverity = ERROR_SEVERITY();  
  RAISERROR(@ErrorMessage, @ErrorSeverity, 1);  
END CATCH;  
  
GO  
EXEC Production.uspDeleteWorkOrder 13;  
  
/* Intentionally generate an error by reversing the order in which rows 
   are deleted from the parent and child tables. This change does not 
   cause an error when the procedure definition is altered, but produces 
   an error when the procedure is executed.  
*/  
ALTER PROCEDURE Production.uspDeleteWorkOrder ( @WorkOrderID int )  
AS  
  
BEGIN TRY  
   BEGIN TRANSACTION   
      -- Delete the rows from the parent table, WorkOrder, for the specified work order.  
   DELETE FROM Production.WorkOrder  
   WHERE WorkOrderID = @WorkOrderID;  
  
   -- Delete rows from the child table, WorkOrderRouting, for the specified work order.  
   DELETE FROM Production.WorkOrderRouting  
   WHERE WorkOrderID = @WorkOrderID;  
  
   COMMIT TRANSACTION  
  
END TRY  
BEGIN CATCH  
  -- Determine if an error occurred.  
  IF @@TRANCOUNT > 0  
     ROLLBACK TRANSACTION  
  
  -- Return the error information.  
  DECLARE @ErrorMessage nvarchar(4000),  @ErrorSeverity int;  
  SELECT @ErrorMessage = ERROR_MESSAGE(),@ErrorSeverity = ERROR_SEVERITY();  
  RAISERROR(@ErrorMessage, @ErrorSeverity, 1);  
END CATCH;  
GO  
-- Execute the altered procedure.  
EXEC Production.uspDeleteWorkOrder 15;  
  
DROP PROCEDURE Production.uspDeleteWorkOrder;  
```  
  
###  <a name="Encrypt"></a>Ofuscando a definição do procedimento  
 Os exemplos desta seção mostram como ofuscar a definição do procedimento armazenado.  
  
#### <a name="k-using-the-with-encryption-option"></a>K. Usando a opção WITH ENCRYPTION  
 O exemplo a seguir cria o procedimento `HumanResources.uspEncryptThis`.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] por meio de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], banco de dados SQL.  
  
```sql  
CREATE PROCEDURE HumanResources.uspEncryptThis  
WITH ENCRYPTION  
AS  
    SET NOCOUNT ON;  
    SELECT BusinessEntityID, JobTitle, NationalIDNumber, 
        VacationHours, SickLeaveHours   
    FROM HumanResources.Employee;  
GO  
```  
  
 O `WITH ENCRYPTION` opção ofusca a definição do procedimento ao consultar o catálogo do sistema ou usando metadados de funções, conforme mostrado nos exemplos a seguir.  
  
 Run `sp_helptext`:  
  
```sql  
EXEC sp_helptext 'HumanResources.uspEncryptThis';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `The text for object 'HumanResources.uspEncryptThis' is encrypted.`  
  
 Consultar diretamente o `sys.sql_modules` exibição do catálogo:  
  
```sql  
SELECT definition FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('HumanResources.uspEncryptThis');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 definition  
 --------------------------------  
 NULL  
 ```  
  
###  <a name="Recompile"></a>Forçar o recompilação do procedimento  
 Os exemplos desta seção usam a cláusula WITH RECOMPILE para forçar a recompilação do procedimento a cada execução.  
  
#### <a name="l-using-the-with-recompile-option"></a>L. Usando a opção WITH RECOMPILE  
 O `WITH RECOMPILE` cláusula é útil quando os parâmetros fornecidos para o procedimento não serão comuns, e quando um novo plano de execução não deve ser armazenados em cache ou armazenado na memória.  
  
```sql  
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
    DROP PROCEDURE dbo.uspProductByVendor;  
GO  
CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
WITH RECOMPILE  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
    FROM Purchasing.Vendor AS v   
    JOIN Purchasing.ProductVendor AS pv   
      ON v.BusinessEntityID = pv.BusinessEntityID   
    JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID  
    WHERE v.Name LIKE @Name;  
```  
  
###  <a name="Security"></a>Definir o contexto de segurança  
 O exemplos desta seção usam a cláusula EXECUTE AS para definir o contexto de segurança no qual o procedimento armazenado é executado.  
  
#### <a name="m-using-the-execute-as-clause"></a>M. Usando a cláusula EXECUTE AS  
 O exemplo a seguir mostra o uso de [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) cláusula para especificar o contexto de segurança no qual um procedimento pode ser executado. No exemplo, a opção `CALLER` Especifica que o procedimento pode ser executado no contexto do usuário que o chama.  
  
```sql  
CREATE PROCEDURE Purchasing.uspVendorAllInfo  
WITH EXECUTE AS CALLER  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS Vendor, p.Name AS 'Product name',   
      v.CreditRating AS 'Rating',   
      v.ActiveFlag AS Availability  
    FROM Purchasing.Vendor v   
    INNER JOIN Purchasing.ProductVendor pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product p  
      ON pv.ProductID = p.ProductID   
    ORDER BY v.Name ASC;  
GO  
```  
  
#### <a name="n-creating-custom-permission-sets"></a>N. Criando conjuntos de permissões personalizados  
 O exemplo a seguir usa EXECUTE AS para criar permissões personalizadas para uma operação de banco de dados. Algumas ações, como TRUNCATE TABLE, não têm permissões concessíveis. Ao incorporar a instrução TRUNCATE TABLE em um procedimento armazenado e especificar que esse procedimento seja executado como um usuário com permissões para modificar a tabela, você pode estender as permissões para truncar a tabela para o usuário ao qual concedeu permissões EXECUTE no procedimento.  
  
```sql  
CREATE PROCEDURE dbo.TruncateMyTable  
WITH EXECUTE AS SELF  
AS TRUNCATE TABLE MyDB..MyTable;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="o-create-a-stored-procedure-that-runs-a-select-statement"></a>O. Criar um procedimento armazenado que executa uma instrução SELECT  
 Este exemplo mostra a sintaxe básica para criar e executar um procedimento. Ao executar um lote, CREATE PROCEDURE deve ser a primeira instrução. Por exemplo criar o seguinte procedimento de armazenado [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)], defina o contexto do banco de dados primeiro e, em seguida, execute a instrução CREATE PROCEDURE.  
  
```sql  
-- Uses AdventureWorksDW database  
  
--Run CREATE PROCEDURE as the first statement in a batch.  
CREATE PROCEDURE Get10TopResellers   
AS   
BEGIN  
    SELECT TOP (10) r.ResellerName, r.AnnualSales  
    FROM DimReseller AS r  
    ORDER BY AnnualSales DESC, ResellerName ASC;  
END  
;  
  
--Show 10 Top Resellers  
EXEC Get10TopResellers;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [Linguagem de controle de fluxo &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [Cursores](../../relational-databases/cursors.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DROP PROCEDURE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [EXECUTE AS &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [Procedimentos armazenados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [sp_procoption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md)   
 [sp_recompile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys.procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [numbered_procedures &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)   
 [numbered_procedure_parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-numbered-procedure-parameters-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [Criar um procedimento armazenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Usar com valor de tabela parâmetros &#40; mecanismo de banco de dados &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
  




