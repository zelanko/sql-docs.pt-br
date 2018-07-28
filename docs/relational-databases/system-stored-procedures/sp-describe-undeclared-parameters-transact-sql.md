---
title: sp_describe_undeclared_parameters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_undeclared_parameters
- sp_describe_undeclared_parameters_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_undeclared_parameters
ms.assetid: 6f016da6-dfee-4228-8b0d-7cd8e7d5a354
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e4a4a97b4a69aaf68d196833ee56b089a3dadfcf
ms.sourcegitcommit: 046d29e700981594725af698a5e079922cf5dbe7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2018
ms.locfileid: "39331582"
---
# <a name="spdescribeundeclaredparameters-transact-sql"></a>sp_describe_undeclared_parameters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  Retorna um conjunto de resultados que contém metadados sobre parâmetros não declarados em um [!INCLUDE[tsql](../../includes/tsql-md.md)] em lotes. Considera cada parâmetro é usado na  **\@tsql** do lote, mas não declarado em  **\@params**. Um conjunto de resultados que contém uma linha para cada um desses parâmetros é retornado com as informações de tipo deduzidas para esse parâmetro. O procedimento retornará um resultado vazio definido se o  **\@tsql** lote de entrada não tem parâmetros, exceto aqueles declarados em  **\@params**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql
  
sp_describe_undeclared_parameters   
    [ @tsql = ] 'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' data type ] [, ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **\@tsql =** ] **'***SQL_batch Transact***'**  
 Uma ou mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. *SQL_batch Transact* pode ser **nvarchar (***n***)** ou **nvarchar (max)**.  
  
 [  **\@params =** ] **N'***parâmetros***'**  
 \@params fornece uma cadeia de caracteres de declaração de parâmetros para o [!INCLUDE[tsql](../../includes/tsql-md.md)] funciona em lotes, da mesma forma que a forma de sp_executesql. *Parâmetros* pode ser **nvarchar (***n***)** ou **nvarchar (max)**.  
  
 É uma cadeia de caracteres que contém as definições de todos os parâmetros que foram inseridos em *SQL_batch Transact*. A cadeia de caracteres deve ser uma constante Unicode ou uma variável Unicode. Cada definição de parâmetro consiste em um nome de parâmetro e um tipo de dados. n é um espaço reservado que indica definições de parâmetro adicionais. Se a instrução Transact-SQL ou lote na instrução não contiver parâmetros, \@params não é necessária. O valor padrão para este parâmetro é NULL.  
  
 Datatype  
 O tipo de dados do parâmetro.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **sp_describe_undeclared_parameters** sempre retorna retorna o status de zero em caso de sucesso. Se o procedimento lançar um erro e o procedimento é chamado como uma RPC, o status de retorno é populado pelo tipo de erro, conforme descrito na coluna error_type de DM exec_describe_first_result_set. Se o procedimento for chamado de [!INCLUDE[tsql](../../includes/tsql-md.md)], o valor de retorno sempre será zero, até mesmo em casos de erro.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_describe_undeclared_parameters** retorna o conjunto de resultados a seguir.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int NOT NULL**|Contém a posição ordinal do parâmetro no conjunto de resultados. A posição do primeiro parâmetro será especificada como 1.|  
|**name**|**sysname NOT NULL**|Contém o nome do parâmetro.|  
|**suggested_system_type_id**|**int NOT NULL**|Contém o **system_type_id** do tipo de dados do parâmetro como especificado em sys. Types.<br /><br /> Para tipos CLR, mesmo que o **system_type_name** coluna retornará NULL, essa coluna retornará o valor 240.|  
|**suggested_system_type_name**|**nvarchar (256) NULL**|Contém o nome do tipo de dados. Inclui argumentos (como comprimento, precisão, escala) especificados para o tipo de dados do parâmetro. Se o tipo de dados for um tipo de alias definido pelo usuário, o tipo de sistema subjacente será especificado aqui. Se for um tipo de dados CLR definido pelo usuário, NULL será retornado nessa coluna. Se não for possível deduzir o tipo de parâmetro, NULL será retornado.|  
|**suggested_max_length**|**smallint não NULL**|Consulte sys. Columns. para **max_length** descrição da coluna.|  
|**suggested_precision**|**tinyint NOT NULL**|Consulte sys. Columns. para obter a descrição da coluna de precisão.|  
|**suggested_scale**|**tinyint NOT NULL**|Consulte sys. Columns. para obter a descrição da coluna de escala.|  
|**suggested_user_type_id**|**int NULL**|Para tipos de CLR e alias, contém o user_type_id do tipo de dados da coluna como especificado em sys.types. Caso contrário, é NULL.|  
|**suggested_user_type_database**|**sysname NULL**|Para tipos de CLR e de alias, contém o nome do banco de dados no qual o tipo é definido. Caso contrário, é NULL.|  
|**suggested_user_type_schema**|**sysname NULL**|Para tipos de CLR e de alias, contém o nome do esquema no qual o tipo é definido. Caso contrário, é NULL.|  
|**suggested_user_type_name**|**sysname NULL**|Para tipos de CLR e de alias, contém o nome do tipo. Caso contrário, é NULL.|  
|**suggested_assembly_qualified_type_name**|**nvarchar (4000) NULL**|Para tipos CLR, retorna o nome do assembly e da classe que define o tipo. Caso contrário, é NULL.|  
|**suggested_xml_collection_id**|**int NULL**|Contém o xml_collection_id do tipo de dados do parâmetro como especificado em sys. Columns. Essa coluna retornará NULL se o tipo retornado não estiver associado uma coleção de esquemas XML.|  
|**suggested_xml_collection_database**|**sysname NULL**|Contém o banco de dados no qual a coleção de esquemas XML associada a esse tipo está definida. Essa coluna retornará NULL se o tipo retornado não estiver associado uma coleção de esquemas XML.|  
|**suggested_xml_collection_schema**|**sysname NULL**|Contém o esquema no qual a coleção de esquemas XML associada a esse tipo está definida. Essa coluna retornará NULL se o tipo retornado não estiver associado uma coleção de esquemas XML.|  
|**suggested_xml_collection_name**|**sysname NULL**|Contém o nome da coleção de esquemas XML associada a esse tipo. Essa coluna retornará NULL se o tipo retornado não estiver associado uma coleção de esquemas XML.|  
|**suggested_is_xml_document**|**bit NOT NULL**|Retornará 1 se o tipo retornado for o XML e esse tipo for, com certeza, um documento XML. Caso contrário, retorna 0.|  
|**suggested_is_case_sensitive**|**bit NOT NULL**|Retornará 1 se a coluna for de um tipo de cadeia de caracteres com diferenciação de maiúsculas e minúsculas e 0 se não for.|  
|**suggested_is_fixed_length_clr_type**|**bit NOT NULL**|Retornará 1 se a coluna for de um tipo de CLR de comprimento fixo e 0 se não for.|  
|**suggested_is_input**|**bit NOT NULL**|Retornará 1 se o parâmetro for usado em qualquer lugar, sem ser o lado esquerdo de uma atribuição. Caso contrário, retorna 0.|  
|**suggested_is_output**|**bit NOT NULL**|Retornará 1 se o parâmetro for usado no lado esquerdo de uma atribuição ou se for transmitido a um parâmetro de saída de um procedimento armazenado. Caso contrário, retorna 0.|  
|**formal_parameter_name**|**sysname NULL**|Se o parâmetro for um argumento para um procedimento armazenado ou uma função definida pelo usuário, retornará o nome do parâmetro formal correspondente. Caso contrário, retornará NULL.|  
|**suggested_tds_type_id**|**int NOT NULL**|Para uso interno.|  
|**suggested_tds_length**|**int NOT NULL**|Para uso interno.|  
  
## <a name="remarks"></a>Remarks  
 **sp_describe_undeclared_parameters** sempre retorna retorna o status de zero.  
  
 O uso mais comum é quando um aplicativo recebe uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que pode conter parâmetros e precisa processá-los de algum modo. Um exemplo é uma interface do usuário (como ODBCTest ou RowsetViewer) onde o usuário fornece uma consulta com sintaxe de parâmetro ODBC. O aplicativo deve descobrir o número de parâmetros dinamicamente e deve solicitar cada parâmetro ao usuário.  
  
 Outro exemplo ocorre quando, sem entrada do usuário, um aplicativo precisa executar um loop dos parâmetros e obter os dados para eles de algum outro local (como uma tabela). Nesse caso, o aplicativo não tem que transmitir todas as informações de parâmetro de uma vez. Em vez disso, o aplicativo pode obter todas as informações de parâmetros do provedor e pode obter os próprios dados na tabela. O código usando **sp_describe_undeclared_parameters** é mais genérico e tem menos probabilidade de requerer modificação se a estrutura de dados as alterações mais tarde.  
  
 **sp_describe_undeclared_parameters** retornará um erro em qualquer um dos casos a seguir.  
  
-   Se a entrada \@tsql não é válido [!INCLUDE[tsql](../../includes/tsql-md.md)] em lotes. Validade é determinada pela análise de [!INCLUDE[tsql](../../includes/tsql-md.md)] em lotes. Os erros causados pelo lote durante a otimização da consulta ou durante a execução não são considerados ao determinar se o [!INCLUDE[tsql](../../includes/tsql-md.md)] lote é válido.  
  
-   Se \@params não for NULL e contém uma cadeia de caracteres que não é uma cadeia de caracteres de declaração sintaticamente válida para parâmetros, ou se ele contiver uma cadeia de caracteres que declare qualquer parâmetro mais de uma vez.  
  
-   Se a entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] lote declara uma variável local de mesmo nome como um parâmetro declarado na \@params.  
  
-   Se a instrução criar qualquer tabela temporária.  
  
 Se \@tsql não tem parâmetros, além daqueles declarados em \@params, o procedimento retornará um conjunto de resultados vazio.  
  
## <a name="parameter-selection-algorithm"></a>Algoritmo de seleção de parâmetro  
 Para uma consulta com parâmetros não declarados, a dedução de tipo de dados para parâmetros não declarados é realizada em três etapas.  
  
 **Etapa 1**  
  
 A primeira etapa na dedução do tipo de dados para uma consulta com parâmetros não declarados é localizar os tipos de dados de todas as subexpressões cujos tipos de dados não dependem de parâmetros não declarados. É possível determinar o tipo para as seguintes expressões:  
  
-   Colunas, constantes, variáveis e parâmetros declarados.  
  
-   Os resultados de uma chamada para uma UDF (função definida pelo usuário).  
  
-   Uma expressão com tipos de dados que não dependem de parâmetros não declarados para todas as entradas.  
  
 Por exemplo, considere a consulta `SELECT dbo.tbl(@p1) + c1 FROM t1 WHERE c2 = @p2 + 2`. As expressões dbo. TBL (\@p1) + c1 e c2 têm tipos de dados e a expressão \@p1 e \@p2 + 2 não têm.  
  
 Depois dessa etapa, se qualquer expressão (sem ser uma chamada para uma UDF) tiver dois argumentos sem tipos de dados, a dedução de tipo falhará com um erro. Por exemplo, os seguintes itens geram erros:  
  
```sql
SELECT * FROM t1 WHERE @p1 = @p2  
SELECT * FROM t1 WHERE c1 = @p1 + @p2  
SELECT * FROM t1 WHERE @p1 = SUBSTRING(@p2, 2, 3)  
```  
  
 O seguinte exemplo não gera um erro:  
  
```sql
SELECT * FROM t1 WHERE @p1 = dbo.tbl(c1, @p2, @p3)  
```
  
 **Etapa 2**  
  
 Para um determinado parâmetro não declarado \@p, o algoritmo de dedução de tipo localiza a expressão interna E (\@p) que contém \@p e é um dos seguintes:  
  
-   Um argumento para um operador comparação ou atribuição.  
  
-   Um argumento para uma função definida pelo usuário (incluindo a UDF com valor de tabela), procedimento ou método.  
  
-   Um argumento para uma **valores** cláusula de uma **inserir** instrução.  
  
-   Um argumento para uma **CAST** ou **converter**.  
  
 O algoritmo de dedução de tipo localiza um tipo de dados de destino TT (\@p) para E (\@p). A seguir são apresentados tipos de dados de destino dos exemplos anteriores:  
  
-   O tipo de dados do outro lado da comparação ou atribuição.  
  
-   O tipo de dados declarado do parâmetro ao qual esse argumento foi passado.  
  
-   O tipo de dados da coluna na qual esse valor é inserido.  
  
-   O tipo de dados no qual a instrução está convertendo.  
  
 Por exemplo, considere a consulta `SELECT * FROM t WHERE @p1 = dbo.tbl(@p2 + c1)`. E, em seguida, (\@p1) = \@p1, E (\@p2) = \@p2 + c1, TT (\@p1) é o tipo de dados de retorno declarado de dbo. TBL e TT (\@p2) é o tipo de dados de parâmetro declarado para dbo. TBL.  
  
 Se \@p não está contida em nenhuma expressão listada no início da etapa 2, o algoritmo de dedução de tipo determinará que E (\@p) é a maior expressão escalar que contém \@p e o algoritmo de dedução de tipo não computação de um tipo de dados de destino TT (\@p) para E (\@p). Por exemplo, se a consulta for SELECT `@p + 2` E, em seguida, (\@p) = \@p + 2, e não há nenhum TT (\@p).  
  
 **Etapa 3**  
  
 Agora que E (\@p) e TT (\@p) são identificados, o algoritmo de dedução de tipo deduz um tipo de dados para \@p de uma das duas maneiras a seguir:  
  
-   Dedução simples  
  
     Se E (\@p) = \@p e TT (\@p) existe, ou seja, se \@p for diretamente um argumento para uma das expressões listadas no início da etapa 2, o algoritmo de dedução de tipo deduz o tipo de dados de \@p para ser (TT \@p). Por exemplo:  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p1 AND @p2 = dbo.tbl(@p3)  
    ```  
  
     O tipo de dados \@p1, \@p2, e \@p3 será o tipo de dados de c1, o tipo de dados de retorno de dbo. TBL, e os dados de parâmetro de tipo para dbo. TBL, respectivamente.  
  
     Como um caso especial, se \@p é um argumento para uma \<, >, \<=, ou > = operador, não se aplicam regras de dedução simples. O algoritmo de dedução de tipo usará as regras de dedução gerais explicadas na próxima seção. Por exemplo, se c1 for uma coluna do tipo de dados char(30), considere as duas consultas a seguir:  
  
    ```sql
    SELECT * FROM t WHERE c1 = @p  
    SELECT * FROM t WHERE c1 > @p  
    ```  
  
     No primeiro caso, o algoritmo de dedução de tipo deduz **char(30)** como o tipo de dados \@p, de acordo com as regras anteriores neste tópico. No segundo caso, o algoritmo de dedução de tipo deduz **varchar(8000)** acordo com as regras de dedução geral na próxima seção.  
  
-   Dedução geral  
  
     Se a dedução simples não for aplicável, os seguintes tipos de dados serão considerados para parâmetros não declarados:  
  
    -   Tipos de dados inteiros (**bits**, **tinyint**, **smallint**, **int**, **bigint**)  
  
    -   Tipos de dados Money (**smallmoney**, **money**)  
  
    -   Tipos de dados de ponto flutuante (**float**, **real**)  
  
    -   **numérico (38, 19)** -outros tipos de dados numéricos ou decimais não são considerados.  
  
    -   **varchar(8000)**, **varchar (max)**, **nvarchar (4000)**, e **nvarchar (max)** - outros tipos de dados de cadeia de caracteres (como **texto**, **char(8000)**, **nvarchar (30)**, etc.) não são considerados.  
  
    -   **varbinary(8000)** e **varbinary (max)** -outros tipos de dados binários não são considerados (como **imagem**, **binary(8000)**, **varbinary (30)** , etc.).  
  
    -   **data**, **time(7)**, **smalldatetime**, **datetime**, **datetime2(7)**, **datetimeoffset(7)**  - Outros de data e hora de tipos, como **time(4)**, não são considerados.  
  
    -   **sql_variant**  
  
    -   **xml**  
  
    -   Tipos CLR definidos pelo sistema (**hierarchyid**, **geometry**, **geografia**)  
  
    -   Tipos definidos pelo usuário de CLR  
  
### <a name="selection-criteria"></a>Critérios de seleção  
 Dos tipos de dados candidatos, qualquer tipo de dados que invalide a consulta será rejeitado. Dos tipos de dados candidatos restantes, o algoritmo de dedução de tipo seleciona um item de acordo com as regras a seguir.  
  
1.  O tipo de dados que produza o menor número de conversões implícitas em E (\@p) é selecionado. Se um determinado tipo de dados produz um tipo de dados para E (\@p) que é diferente de TT (\@p), o algoritmo de dedução de tipo considerará isso uma conversão implícita extra do tipo de dados de E (\@p) para TT (\@p).  
  
     Por exemplo:  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_Int + @p  
    ```  
  
     Nesse caso, E (\@p) é Col_Int + \@p e TT (\@p) é **int**. **int** é escolhido para \@p porque ele não produz conversões implícitas. Qualquer outra escolha de tipo de dados gera uma conversão implícita pelo menos.  
  
2.  Se houver vários tipos de dados ligados ao menor número de conversões, o tipo de dados com a precedência mais alta será usada. Por exemplo  
  
    ```sql
    SELECT * FROM t WHERE Col_Int = Col_smallint + @p  
    ```  
  
     Nesse caso, **int** e **smallint** geram uma conversão. Todos os outros tipos de dados geram mais de uma conversão. Porque **int** prevalece sobre **smallint**, **int** é usado para \@p. Para obter mais informações sobre a precedência de tipo de dados, consulte [precedência de tipo de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-precedence-transact-sql.md).  
  
     Essa regra somente se aplicará se houver uma conversão implícita entre cada tipo de dados ligado de acordo com regra 1 e o tipo de dados com a precedência mais alta. Se não houver nenhuma conversão implícita, a dedução de tipo de dados falhará com um erro. Por exemplo, na consulta `SELECT @p FROM t`, falha de dedução de tipo de dados porque qualquer tipo de dados para \@p seria igualmente bom. Por exemplo, não há nenhuma conversão implícita de **int** à **xml**.  
  
3.  Se dois tipos de dados semelhantes ligados de acordo com regra 1, por exemplo **varchar(8000)** e **varchar (max)**, o menor tipo de dados (**varchar(8000)**) é escolhido. O mesmo princípio se aplica ao **nvarchar** e **varbinary** tipos de dados.  
  
4.  Para os propósitos da regra 1, o algoritmo de dedução de tipo considera certas conversões melhores que outras. As conversões, na ordem da melhor para a pior são:  
  
    1.  Conversão entre o mesmo tipo de dados básico de comprimento diferente.  
  
    2.  Conversão entre a versão de comprimento fixo e comprimento variável dos mesmos tipos de dados (por exemplo, **char** à **varchar**).  
  
    3.  Conversão entre **nulo** e **int**.  
  
    4.  Qualquer outra conversão.  
  
 Por exemplo, para a consulta `SELECT * FROM t WHERE [Col_varchar(30)] > @p`, **varchar(8000)** é escolhido como conversão (a) é melhor. Para a consulta `SELECT * FROM t WHERE [Col_char(30)] > @p`, **varchar(8000)** ainda será escolhido porque causa uma conversão de tipo (b) e porque outra escolha (como **varchar(4000)**) causaria uma conversão de tipo (d).  
  
 Como um exemplo final, dada uma consulta `SELECT NULL + @p`, **int** é escolhido para \@p porque resulta em uma conversão de tipo (c).  
  
## <a name="permissions"></a>Permissões  
 Requer permissão para executar o \@argumento tsql.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações como o tipo de dados esperado para os parâmetros não declarados `@id` e `@name`.  
  
```sql
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR name = @name'  
  
```  
  
 Quando o parâmetro `@id` é fornecido como uma referência `@params`, o parâmetro `@id` é omitido do conjunto de resultados e somente o parâmetro `@name` é descrito.  
  
```sql
sp_describe_undeclared_parameters @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes  
WHERE object_id = @id OR NAME = @name',  
@params = N'@id int'  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)