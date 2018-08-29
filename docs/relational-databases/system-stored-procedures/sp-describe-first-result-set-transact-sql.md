---
title: sp_describe_first_result_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_describe_first_result_set
- sp_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_describe_first_result_set
ms.assetid: f2355a75-3a8e-43e6-96ad-4f41038f6d22
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 03d40263e27c16dcf3eff5300f942f3deb295bd9
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43099102"
---
# <a name="spdescribefirstresultset-transact-sql"></a>sp_describe_first_result_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Retorna os metadados para o primeiro resultado possível conjunto do [!INCLUDE[tsql](../../includes/tsql-md.md)] em lotes. Retorna um conjunto de resultados vazio quando o lote não retorna resultados. Gera um erro se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não é possível determinar os metadados para a primeira consulta que será executada por meio de uma análise estática. O modo de exibição de gerenciamento dinâmico [DM exec_describe_first_result_set &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md) retorna as mesmas informações.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_describe_first_result_set [ @tsql = ] N'Transact-SQL_batch'   
    [ , [ @params = ] N'parameters' ]   
    [ , [ @browse_information_mode = ] <tinyint> ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **\@tsql =** ] **'***SQL_batch Transact***'**  
 Uma ou mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. *SQL_batch Transact* pode ser **nvarchar (***n***)** ou **nvarchar (max)**.  
  
 [  **\@params =** ] **N'***parâmetros***'**  
 \@params fornece uma cadeia de caracteres de declaração de parâmetros para o [!INCLUDE[tsql](../../includes/tsql-md.md)] lote, que é similar a sp_executesql. Parâmetros podem ser **nvarchar (n)** ou **nvarchar (max)**.  
  
 É uma cadeia de caracteres que contém as definições de todos os parâmetros que foram inseridos na [!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*. A cadeia de caracteres deve ser uma constante Unicode ou uma variável Unicode. Cada definição de parâmetro consiste em um nome de parâmetro e um tipo de dados. *n* é um espaço reservado que indica definições de parâmetro adicionais. Todo parâmetro especificado na instrução deve ser definido em \@params. Se o [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou lote na instrução não contiverem parâmetros, \@params não é necessária. NULL é o valor padrão para esse parâmetro.  
  
 [  **\@browse_information_mode =** ] *tinyint*  
 Especifica se colunas de chave adicionais e informações de tabela de origem são retornadas. Se definido como 1, cada consulta será analisada como se incluísse uma opção FOR BROWSE na consulta. Colunas de chave adicionais e informações de tabela de origem são retornadas.  
  
-   Se for definido como 0, nenhuma informação será retornada.  
  
-   Se definido como 1, cada consulta será analisada como se incluísse uma opção FOR BROWSE na consulta. Isto retornará nomes de tabela base como as informações de coluna de origem.  
  
-   Se for definido como 2, cada consulta será analisada como se fosse usada na preparação ou execução de um cursor. Isto retornará nomes de exibição como as informações de coluna de origem.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **sp_describe_first_result_set** sempre retorna um status de zero em caso de sucesso. Se o procedimento lançar um erro e o procedimento é chamado como uma RPC, o status de retorno é populado pelo tipo de erro descrito na coluna error_type de DM exec_describe_first_result_set. Se o procedimento for chamado de [!INCLUDE[tsql](../../includes/tsql-md.md)], o valor de retorno sempre será zero, até mesmo se houver erro.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Estes metadados comuns são retornados como um conjunto de resultados com uma linha para cada coluna nos metadados de resultados. Cada linha descreve o tipo e a nulidade da coluna no formato descrito na seção a seguir. Se a primeira instrução não existir para todo caminho de controle, um conjunto de resultados com zero linhas será retornado.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit NOT NULL**|Indica que a coluna é uma coluna extra adicionada para fins de informações de navegação e que ela não é exibida realmente no conjunto de resultados.|  
|**column_ordinal**|**int NOT NULL**|Contém a posição ordinal da coluna no conjunto de resultados. A posição da primeira coluna será especificada como 1.|  
|**name**|**sysname NULL**|Conterá o nome da coluna se um nome puder ser determinado. Caso contrário, conterá NULL.|  
|**is_nullable**|**bit NOT NULL**|Conterá o valor 1 se a coluna permitir NULLs, 0 se a coluna não permitir NULLs e 1 caso não seja possível determinar se a coluna permite NULLs.|  
|**system_type_id**|**int NOT NULL**|Contém o system_type_id do tipo de dados da coluna como especificado em sys. Types. Para tipos de CLR, embora a coluna system_type_name retorne NULL, essa coluna retornará o valor 240.|  
|**system_type_name**|**nvarchar(256) NULL**|Contém o nome e argumentos (como comprimento, precisão, escala), especificados para o tipo de dados da coluna. Se o tipo de dados for um tipo de alias definido pelo usuário, o tipo de sistema subjacente será especificado aqui. Se for um tipo de CLR definido pelo usuário, NULL será retornado nessa coluna.|  
|**max_length**|**smallint não NULL**|Comprimento máximo (em bytes) da coluna.<br /><br /> -1 = a coluna é do tipo de dados **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, ou **xml**.<br /><br /> Para **texto** colunas, o **max_length** valor será 16 ou o valor definido pelo **sp_tableoption 'text in row'**.|  
|**Precisão**|**tinyint NOT NULL**|Precisão da coluna, se tiver base numérica. Caso contrário, retorna 0.|  
|**scale**|**tinyint NOT NULL**|Escala da coluna, se tiver base numérica. Caso contrário, retorna 0.|  
|**collation_name**|**sysname NULL**|Nome do agrupamento da coluna, se baseada em caracteres. Caso contrário, retornará NULL.|  
|**user_type_id**|**int NULL**|Para tipos de CLR e alias, contém o user_type_id do tipo de dados da coluna como especificado em sys.types. Caso contrário, é NULL.|  
|**user_type_database**|**sysname NULL**|Para tipos de CLR e de alias, contém o nome do banco de dados no qual o tipo é definido. Caso contrário, é NULL.|  
|**user_type_schema**|**sysname NULL**|Para tipos de CLR e de alias, contém o nome do esquema no qual o tipo é definido. Caso contrário, é NULL.|  
|**user_type_name**|**sysname NULL**|Para tipos de CLR e de alias, contém o nome do tipo. Caso contrário, é NULL.|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|Para tipos de CLR, retorna o nome do assembly e da classe que define o tipo. Caso contrário, é NULL.|  
|**xml_collection_id**|**int NULL**|Contém o xml_collection_id do tipo de dados da coluna como especificado em sys.columns. Essa coluna retornará NULL se o tipo retornado não estiver associado uma coleção de esquemas XML.|  
|**xml_collection_database**|**sysname NULL**|Contém o banco de dados no qual a coleção de esquemas XML associada a esse tipo está definida. Essa coluna retornará NULL se o tipo retornado não estiver associado uma coleção de esquemas XML.|  
|**xml_collection_schema**|**sysname NULL**|Contém o esquema no qual a coleção de esquemas XML associada a esse tipo está definida. Essa coluna retornará NULL se o tipo retornado não estiver associado uma coleção de esquemas XML.|  
|**xml_collection_name**|**sysname NULL**|Contém o nome da coleção de esquemas XML associada a esse tipo. Essa coluna retornará NULL se o tipo retornado não estiver associado uma coleção de esquemas XML.|  
|**is_xml_document**|**bit NOT NULL**|Retornará 1 se o tipo de dados retornado for o XML e esse tipo for garantido de ser um documento XML completo (incluindo um nó raiz), em vez de um fragmento XML. Caso contrário, retorna 0.|  
|**is_case_sensitive**|**bit NOT NULL**|Retornará 1 se a coluna for um tipo de cadeia de caracteres com diferenciação de maiúsculas e minúsculas; caso contrário, retornará 0.|  
|**is_fixed_length_clr_type**|**bit NOT NULL**|Retornará 1 se a coluna for um tipo de CLR de comprimento fixo; caso contrário, retornará 0.|  
|**source_server**|**sysname**|Nome do servidor de origem retornado pela coluna neste resultado (se a origem for um servidor remoto). O nome é fornecido como ele aparece em sys. Servers. Retornará NULL se a coluna tiver origem no servidor local ou caso não seja possível determinar o servidor de origem. É populado somente se informações de navegação são solicitadas.|  
|**source_database**|**sysname**|Nome do banco de dados de origem retornado pela coluna neste resultado. Retornará NULL se o banco de dados não puder ser determinado. É populado somente se informações de navegação são solicitadas.|  
|**source_schema**|**sysname**|Nome do esquema de origem retornado pela coluna neste resultado. Retornará NULL se o esquema não puder ser determinado. É populado somente se informações de navegação são solicitadas.|  
|**source_table**|**sysname**|Nome da tabela de origem retornado pela coluna neste resultado. Retornará NULL se a tabela não puder ser determinada. É populado somente se informações de navegação são solicitadas.|  
|**source_column**|**sysname**|Nome da coluna de origem retornado pela coluna de resultado. Retornará NULL se a coluna não puder ser determinada. É populado somente se informações de navegação são solicitadas.|  
|**is_identity_column**|**bit nulo**|Retornará 1 se a coluna for uma coluna de identidade; caso contrário, retornará 0. Retornará NULL caso não seja possível determinar se a coluna é uma coluna de identidade.|  
|**is_part_of_unique_key**|**bit nulo**|Retornará 1 se a coluna fizer parte de um índice exclusivo (incluindo restrição exclusiva e primária); caso contrário, retornará 0. Retornará NULL caso não seja possível determinar se a coluna faz parte de um índice exclusivo. Será populado somente se informações de navegação forem solicitadas.|  
|**is_updateable**|**bit nulo**|Retornará 1 se a coluna for uma coluna atualizável; caso contrário, retornará 0. Retornará NULL caso não seja possível determinar se a coluna é atualizável.|  
|**is_computed_column**|**bit nulo**|Retornará 1 se a coluna for uma coluna computada; caso contrário, retornará 0. Retorna NULL se não puder ser determinado que a coluna é uma coluna computada.|  
|**is_sparse_column_set**|**bit nulo**|Retornará 1 se a coluna for uma coluna esparsa; caso contrário, retornará 0. Retorna NULL se não puder ser determinado que a coluna faz parte de um conjunto de colunas esparsas.|  
|**ordinal_in_order_by_list**|**smallint NULL**|Posição desta coluna na lista ORDER BY. Retornará NULL se a coluna não aparecer na lista ORDER BY ou se a lista ORDER BY não puder ser determinada exclusivamente.|  
|**order_by_list_length**|**smallint NULL**|Comprimento da lista ORDER BY. Retornará NULL se não houver uma lista ORDER BY ou se a lista ORDER BY não puder ser determinada exclusivamente. Observe que esse valor será o mesmo para todas as linhas retornadas por **sp_describe_first_result_set.**|  
|**order_by_is_descending**|**smallint NULL**|Se o ordinal_in_order_by_list não for nulo, o **order_by_is_descending** coluna relatará a direção da cláusula ORDER BY para esta coluna. Caso contrário, relatará NULL.|  
|**tds_type_id**|**int NOT NULL**|Para uso interno.|  
|**tds_length**|**int NOT NULL**|Para uso interno.|  
|**tds_collation_id**|**int NULL**|Para uso interno.|  
|**tds_collation_sort_id**|**tinyint NULL**|Para uso interno.|  
  
## <a name="remarks"></a>Remarks  
 **sp_describe_first_result_set** garantias de que se o procedimento retorna os metadados do primeiro conjunto de resultados para (um controle) em lotes A e, se esse lote (A) for subsequentemente executado, em seguida, o lote serão de (1) gerará um erro de tempo de otimização, (2) gera um erro de tempo de execução, (3) não retornará nenhum resultado definida, ou (4) retorna um primeiro conjunto de resultados com os mesmos metadados descritos por **sp_describe_first_result_set**.  
  
 O nome, a nulidade e o tipo de dados podem diferir. Se **sp_describe_first_result_set** retorna um conjunto de resultados vazio, a garantia é que a execução de lote retornará conjuntos sem resultados.  
  
 Essa garantia presume que não existem alterações de esquema relevantes no servidor. Alterações de esquema relevantes no servidor não incluem a criação de tabelas temporárias ou variáveis de tabela no lote A entre a hora em que **sp_describe_first_result_set** é chamado e a hora em que o conjunto de resultados é retornado durante execução, incluindo alterações de esquema feitas pelo lote B.  
  
 **sp_describe_first_result_set** retornará um erro em qualquer um dos casos a seguir.  
  
-   Se a entrada \@tsql não é válido [!INCLUDE[tsql](../../includes/tsql-md.md)] em lotes. Validade é determinada pela análise de [!INCLUDE[tsql](../../includes/tsql-md.md)] em lotes. Os erros causados pelo lote durante a otimização da consulta ou durante a execução não são considerados ao determinar se o [!INCLUDE[tsql](../../includes/tsql-md.md)] lote é válido.  
  
-   Se \@params não for NULL e contém uma cadeia de caracteres que não é uma cadeia de caracteres de declaração sintaticamente válida para parâmetros, ou se ele contiver uma cadeia de caracteres que declare qualquer parâmetro mais de uma vez.  
  
-   Se a entrada [!INCLUDE[tsql](../../includes/tsql-md.md)] lote declara uma variável local de mesmo nome como um parâmetro declarado na \@params.  
  
-   Se a instrução usar uma tabela temporária.  
  
-   A consulta inclui a criação de uma tabela permanente que é então consultada.  
  
 Se todas as outras verificações forem bem-sucedidas, serão considerados todos os caminhos de fluxo de controle possíveis dentro do lote de entrada. Esse leva em conta o controle de todas as instruções de fluxo (GOTO, IF/ELSE, WHILE, e [!INCLUDE[tsql](../../includes/tsql-md.md)] blocos TRY/CATCH), bem como quaisquer procedimentos, dinâmicos [!INCLUDE[tsql](../../includes/tsql-md.md)] lotes ou invocados de lote de entrada por uma instrução EXEC, uma instrução DDL que faz com que os gatilhos Gatilhos DDL deve ser acionado, ou uma instrução DML que faz com que os gatilhos ser acionado em uma tabela de destino ou em uma tabela que é modificada por causa de ação em cascata em uma restrição foreign key. No caso de muitos possíveis caminhos de controle, em algum ponto, um algoritmo para.  
  
 Para cada caminho de fluxo de controle, a primeira instrução (se houver) que retorna um conjunto de resultados é determinado pela **sp_describe_first_result_set**.  
  
 Quando houver várias e possíveis primeiras instruções em um lote, seus resultados podem diferir no número de colunas, no nome da coluna, na nulidade e no tipo de dados. Veja aqui mais detalhadamente como essas diferenças são tratadas:  
  
-   Se o número de colunas diferir, um erro será gerado e nenhum resultado será retornado.  
  
-   Se o nome da coluna diferir, o nome da coluna retornado será definido como NULL.  
  
-   Se a nulidade diferir, a nulidade retornada permitirá NULLs.  
  
-   Se o tipo de dados diferir, um erro será gerado e nenhum resultado será retornado, exceto nos seguintes casos:  
  
    -   **varchar(a)** à **varchar(a')** onde um ' > um.  
  
    -   **varchar(a)** para **varchar (max)**  
  
    -   **nvarchar(a)** à **nvarchar(a')** onde um ' > um.  
  
    -   **nvarchar(a)** para **nvarchar (max)**  
  
    -   **varbinary(a)** à **varbinary(a')** onde um ' > um.  
  
    -   **varbinary(a)** para **varbinary (max)**  
  
 **sp_describe_first_result_set** não oferece suporte a recursão indireta.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão para executar o \@argumento tsql.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="typical-examples"></a>Exemplos típicos  
  
#### <a name="a-simple-example"></a>A. Exemplo simples  
 O exemplo a seguir descreve o conjunto de resultados retornado de uma única consulta.  
  
```  
sp_describe_first_result_set @tsql = N'SELECT object_id, name, type_desc FROM sys.indexes'  
```  
  
 O exemplo a seguir mostra o conjunto de resultados retornado de uma única consulta que contém um parâmetro.  
  
```  
sp_describe_first_result_set @tsql =   
N'SELECT object_id, name, type_desc   
FROM sys.indexes   
WHERE object_id = @id1'  
, @params = N'@id1 int'  
```  
  
#### <a name="b-browse-mode-examples"></a>B. Exemplos do modo de procura  
 Os três exemplos a seguir ilustram a principal diferença entre os modos de procurar informações. Somente as colunas relevantes foram incluídas nos resultados da consulta.  
  
 Exemplo que usa 0 indicando que nenhuma informação foi retornada.  
  
```sql  
CREATE TABLE dbo.t (a int PRIMARY KEY, b1 int);  
GO  
CREATE VIEW dbo.v AS SELECT b1 AS b2 FROM dbo.t;  
GO  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM dbo.v', null, 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|nome|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|NULL|NULL|NULL|NULL|  
  
 Exemplo que usa 1 indicando que retorna informações como se incluísse uma opção FOR BROWSE na consulta.  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 1  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|nome|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|b3|dbo|t|B1|0|  
|1|2|a|dbo|t|a|1|  
  
 Exemplo que usa 2 indicando que foi analisado como se você estivesse preparando um cursor.  
  
```sql  
EXEC sp_describe_first_result_set N'SELECT b2 AS b3 FROM v', null, 2  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|is_hidden|column_ordinal|nome|source_schema|source_table|source_column|is_part_of_unique_key|  
|----------------|---------------------|----------|--------------------|-------------------|--------------------|-------------------------------|  
|0|1|B3|dbo|v|B2|0|  
|1|2|ROWSTAT|NULL|NULL|NULL|0|  
  
### <a name="examples-of-problems"></a>Exemplos de problemas  
 Os exemplos a seguir usam duas tabelas para todos os exemplos. Execute as seguintes instruções para criar as tabelas de exemplo.  
  
```  
CREATE TABLE dbo.t1 (a int NULL, b varchar(10) NULL, c nvarchar(10) NULL);  
CREATE TABLE dbo.t2 (a smallint NOT NULL, d varchar(20) NOT NULL, e int NOT NULL);  
```  
  
#### <a name="error-because-the-number-of-columns-differ"></a>Erro porque o número de colunas difere  
 O número de colunas nos possíveis primeiros conjuntos de resultados difere neste exemplo.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a, b FROM t1;  
SELECT * FROM t; -- Ignored, not a possible first result set.'  
  
```  
  
#### <a name="error-because-the-data-types-differ"></a>Erro porque os tipos de dados diferem  
 Os tipos de colunas diferem nos primeiros possíveis conjuntos de resultados diferentes.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT a FROM t1;  
ELSE  
    SELECT a FROM t2;  
```  
  
 Resultado: Erro, tipos incompatíveis (**int** versus **smallint**).  
  
#### <a name="column-name-cannot-be-determined"></a>O nome da coluna não pode ser determinado  
 As colunas nos primeiros possíveis conjuntos de resultados diferem no comprimento para o mesmo tipo de comprimento variável, nulidade e nomes de coluna:  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d FROM t2; '  
```  
  
 Resultado: \<nome de coluna desconhecido > **varchar(20) NULL**  
  
#### <a name="column-name-forced-to-be-identical-through-aliasing"></a>Nome de coluna forçado a ser idêntico via alias  
 Igual ao anterior, mas as colunas têm o mesmo nome via alias de coluna.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT d AS b FROM t2;'  
```  
  
 Resultado: b **varchar (20) NULL**  
  
#### <a name="error-because-column-types-cannot-be-matched"></a>Erro porque os tipos de coluna não podem ser correspondidos  
 Os tipos de coluna diferem nos primeiros possíveis conjuntos de resultados diferentes.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    SELECT b FROM t1;  
ELSE  
    SELECT c FROM t1;'  
```  
  
 Resultado: Erro, tipos incompatíveis (**varchar(10)** versus **nvarchar (10)**).  
  
#### <a name="result-set-can-return-an-error"></a>O conjunto de resultados pode retornar um erro  
 O primeiro conjunto de resultados é erro ou conjunto de resultados.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RAISERROR(''Some Error'', 16, 1);  
  
ELSE  
    SELECT a FROM t1;  
SELECT e FROM t2; -- Ignored, not a possible first result set.;'  
```  
  
 Resultado: um **intNULL**  
  
#### <a name="some-code-paths-return-no-results"></a>Alguns caminhos de código não retornam resultados  
 O primeiro conjunto de resultados é nulo ou um conjunto de resultados.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
IF(1=1)  
    RETURN;  
SELECT a FROM t1;'  
```  
  
 Resultado: um **intNULL**  
  
#### <a name="result-from-dynamic-sql"></a>Resultado do SQL dinâmico  
 O primeiro conjunto de resultados é SQL dinâmico, detectável porque é cadeia de caracteres literal.  
  
```  
sp_describe_first_result_set @tsql =   
N'EXEC(N''SELECT a FROM t1'');'  
```  
  
 Resultado: um **INT NULL**  
  
#### <a name="result-failure-from-dynamic-sql"></a>Falha no resultado do SQL dinâmico  
 O primeiro conjunto de resultados é indefinido devido ao SQL dinâmico.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL); '  
```  
  
 Resultado: Erro. O resultado não é detectável devido ao SQL dinâmico.  
  
#### <a name="result-set-specified-by-user"></a>Conjunto de resultados especificado por usuário  
 O primeiro conjunto de resultados é especificado manualmente pelo usuário.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
DECLARE @SQL NVARCHAR(max);  
SET @SQL = N''SELECT a FROM t1 WHERE 1 = 1 '';  
IF(1=1)  
    SET @SQL += N'' AND e > 10 '';  
EXEC(@SQL)  
    WITH RESULT SETS(  
        (Column1 BIGINT NOT NULL)  
    ); '  
```  
  
 Resultado: Coluna1 **bigint NOT NULL**  
  
#### <a name="error-caused-by-a-ambiguous-result-set"></a>Erro causado por um conjunto de resultados ambíguo  
 Este exemplo supõe que o outro usuário nomeado Usuário1 tem uma tabela nomeada t1 no esquema padrão s1 com colunas (uma **int NOT NULL**).  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT * FROM t1;'  
, @params = N'@p int'  
```  
  
 Resultado: Erro. T1 pode ser dbo.t1 ou s1.t1, cada um com um número diferente de colunas.  
  
#### <a name="result-even-with-ambiguous-result-set"></a>Resulta até mesmo com um conjunto de resultados ambíguo  
 Use as mesmas suposições do exemplo anterior.  
  
```  
sp_describe_first_result_set @tsql =   
N'  
    IF(@p > 0)  
    EXECUTE AS USER = ''user1'';  
    SELECT a FROM t1;'  
```  
  
 Resultado: uma **int NULL** porque dbo.t1.a e s1.t1.a têm o tipo **int** e nulidade diferente.  
  
## <a name="see-also"></a>Consulte também  
 [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)   
 [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
 
