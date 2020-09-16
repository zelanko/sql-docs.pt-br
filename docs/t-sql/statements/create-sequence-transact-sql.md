---
description: CREATE SEQUENCE (Transact-SQL)
title: CREATE SEQUENCE (Transact-SQL)
ms.custom: ''
ms.date: 04/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SEQUENCE
- CREATE SEQUENCE
- SEQUENCE_TSQL
- CREATE_SEQUENCE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SEQUENCE statement
- sequence number object, creating
- sequence object
- number, sequence
ms.assetid: 419f907b-8a72-4d6c-80cb-301df44c24c1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8eb9c50b7c30a53265c22b29d616ef3471515ea3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547803"
---
# <a name="create-sequence-transact-sql"></a>CREATE SEQUENCE (Transact-SQL)

[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  Cria um objeto de sequência e especifica suas propriedades. Uma sequência é um objeto associado a um esquema definido pelo usuário que gera uma sequência de valores numéricos de acordo com a especificação com a qual a sequência foi criada. A sequência de valores numéricos é gerada em ordem crescente ou decrescente em um intervalo definido e pode ser configurada para reiniciar (em um ciclo) quando se esgotar. As sequências, ao contrário de colunas de identidade, não são associadas a tabelas específicas. Os aplicativos fazem referência a um objeto de sequência para recuperar seu próximo valor. A relação entre sequências e tabelas é controlada pelo aplicativo. Os aplicativos de usuário podem referenciar um objeto de sequência e coordenar os valores nas várias linhas e tabelas.  
  
 Ao contrário de valores de colunas de identidade que são gerados quando as linhas são inseridas, um aplicativo pode obter o próximo número de sequência sem inserir a linha por meio da chamada da [função NEXT VALUE FOR](../../t-sql/functions/next-value-for-transact-sql.md). Use [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) para obter vários números de sequência de uma vez.  
  
 Para obter informações e cenários que usam **CREATE SEQUENCE** e a função **NEXT VALUE FOR** , consulte [Números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CREATE SEQUENCE [schema_name . ] sequence_name  
    [ AS [ built_in_integer_type | user-defined_integer_type ] ]  
    [ START WITH <constant> ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE [ <constant> ] } | { NO MINVALUE } ]  
    [ { MAXVALUE [ <constant> ] } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*sequence_name*  
Especifica o nome exclusivo pelo qual a sequência é conhecida no banco de dados. O tipo é **sysname**.  
  
[ built_in_integer_type | user-defined_integer_type  
Uma sequência pode ser definida como qualquer tipo de inteiro. Os seguintes tipos são permitidos:  
  
-   **tinyint** – intervalo de 0 a 255  
-   **smallint** – intervalo de -32.768 a 32.767  
-   **int** – intervalo de -2.147.483.648 a 2.147.483.647  
-   **bigint** – intervalo -9.223.372.036.854.775.808 a 9.223.372.036.854.775.807  
-   **decimal** e **numeric** com uma escala de 0.  
-   Qualquer tipo de dados definido pelo usuário (tipo de alias) que seja baseado em um dos tipos permitidos.  
  
Se nenhum tipo de dados for fornecido, o tipo de dados **bigint** será usado como o padrão.  
  
START WITH \<constant>  
O primeiro valor retornado pelo objeto de sequência. O valor **START** deve ser menor ou igual ao valor máximo e maior ou igual ao valor mínimo do objeto de sequência. O valor de início padrão para um novo objeto de sequência é o valor mínimo para um objeto de sequência e o valor máximo de um objeto de sequência decrescente.  
  
INCREMENT BY \<constant>  
O valor usado para incrementar (ou decrementar, se negativo) o valor do objeto de sequência para cada chamada da função **NEXT VALUE FOR**. Se o incremento for um valor negativo, o objeto de sequência será decrescente, caso contrário, será crescente. O incremento não pode ser 0. O incremento padrão para um novo objeto de sequência é 1.  
  
[ MINVALUE \<constant> | **NO MINVALUE** ]  
Especifica os limites do objeto de sequência. O valor mínimo padrão de um novo objeto de sequência é o valor mínimo do tipo de dados do objeto de sequência. É zero para o tipo de dados **tinyint** e um número negativo para todos os outros tipos de dados.  
  
[ MAXVALUE \<constant> | **NO MAXVALUE**  
Especifica os limites do objeto de sequência. O valor máximo padrão para um novo objeto de sequência é o valor máximo do tipo de dados do objeto de sequência.  
  
[ CYCLE | **NO CYCLE** ]  
Propriedade que especifica se o objeto de sequência deve reiniciar do valor mínimo (ou máximo para objetos de sequência decrescente) ou deve lançar uma exceção quando seu valor mínimo ou máximo é excedido. A opção de ciclo padrão para novos objetos de sequência é NO CYCLE.  
  
> [!NOTE]
> Clicar em SEQUENCE reinicia do valor mínimo ou máximo, não do valor inicial.  
  
[ **CACHE** [\<constant> ] | NO CACHE ]  
Aumenta o desempenho de aplicativos que usam objetos de sequência por meio da minimização do número de E/S de disco necessárias para gerar números de sequência. Padrões para o CACHE.  
  
Por exemplo, se um tamanho de cache de 50 for escolhido, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não manterá 50 valores individuais em cache. Somente permanecem em cache o valor atual e o número de valores restantes no cache. Isso significa que a quantidade de memória necessária para armazenar o cache sempre é duas instâncias do tipo de dados do objeto de sequência.  
  
> [!NOTE]  
> Se a opção de cache for habilitada sem a especificação de um tamanho de cache, o Mecanismo de Banco de Dados selecionará um tamanho. Porém, os usuários não devem confiar que a seleção será consistente. [!INCLUDE[msCoName](../../includes/msconame-md.md)] pode alterar o método de cálculo do tamanho do cache sem aviso prévio.  
  
Quando criado com a opção **CACHE**, um desligamento inesperado (uma falta de energia, por exemplo) pode acarretar a perda dos números de sequência restantes no cache.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Os números de sequência são gerados fora do escopo da transação atual. Eles serão consumidos se a transação que usa o número de sequência for confirmada ou revertida. A validação duplicada só ocorre quando o registro está totalmente preenchido. Isso pode resultar em alguns casos em que o mesmo número é usado para mais de um registro durante a criação, mas em seguida é identificado como uma duplicata. Se isso ocorrer e outros valores de numeração automática tiverem sido aplicados a registros subsequentes, o resultado poderá ser um intervalo entre os valores de numeração automática, um comportamento esperado.
  
### <a name="cache-management"></a>Gerenciamento de cache  
 Para aprimorar o desempenho, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pré-aloca o número de números de sequência especificado pelo argumento **CACHE**.  
  
 Por exemplo, uma nova sequência é criada com um valor inicial de 1 e um tamanho de cache de 15. Quando o primeiro valor é necessário, valores de 1 a 15 são disponibilizados da memória. O último valor em cache (15) é gravado nas tabelas do sistema no disco. Quando todos os 15 números são usados, a solicitação seguinte (pelo número 16) faz com que o cache seja alocado novamente. O novo valor colocado no cache por último (30) será gravado nas tabelas do sistema.  
  
 Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for interrompido depois que você usar 22 números, o próximo número de sequência pretendido na memória (23) será gravado nas tabelas do sistema, substituindo o número armazenado antes.  
  
 Após a reinicialização do SQL Server e quando um número de sequência for necessário, o número inicial será lido nas tabelas do sistema (23). A quantidade de cache de 15 números (23-38) é alocada para a memória e o próximo número não de cache (39) é gravado nas tabelas do sistema.  
  
 Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] parar de modo anormal para um evento, como uma falha de energia, a sequência reiniciará com o número lido nas tabelas do sistema (39). Todos os números de sequência alocados à memória (mas nunca solicitados por um usuário ou aplicativo) são perdidos. Essa funcionalidade pode deixar intervalos, mas garante que o mesmo valor nunca seja emitido duas vezes para um único objeto de sequência, a menos que seja definido como **CYCLE** ou reiniciado manualmente.  
  
 O cache é mantido na memória por meio do acompanhamento do valor atual (o último valor emitido) e o número de valores restantes no cache. Portanto, a quantidade de memória usada pelo cache sempre é duas instâncias do tipo de dados do objeto de sequência.  
  
 A configuração do argumento de cache como **NO CACHE** grava o valor de sequência atual nas tabelas do sistema sempre que uma sequência é usada. Isso pode prejudicar o desempenho ao aumentar o acesso ao disco, mas reduz a possibilidade de intervalos não intencionais. Ainda poderão ocorrer intervalos se os números forem solicitados com o uso das funções **NEXT VALUE FOR** ou **sp_sequence_get_range**, mas, neste caso, os números não são usados ou são utilizados em transações não confirmadas.  
  
 Quando um objeto de sequência usa a opção **CACHE**, se você reiniciar esse objeto ou alterar **INCREMENT**, **CYCLE**, **MINVALUE**, **MAXVALUE** ou as propriedades de tamanho de cache, isso fará com que o cache seja gravado nas tabelas do sistema, antes da alteração. Em seguida, o cache é recarregado a partir do valor atual (ou seja, nenhum número é ignorado). A alteração do tamanho do cache entra em vigor imediatamente.  
  
 **Opção CACHE quando os valores em cache estão disponíveis**  
  
 O processo a seguir ocorre sempre que um objeto de sequência recebe uma solicitação para gerar o próximo valor para a opção **CACHE**, caso haja valores não usados disponíveis no cache na memória para o objeto de sequência.  
  
1.  O próximo valor para o objeto de sequência é calculado.  
  
2.  O novo valor atual para o objeto de sequência é atualizado na memória.  
  
3.  O valor calculado é retornado à instrução de chamada.  
  
**Opção CACHE quando o cache está esgotado**  
  
 O seguinte processo ocorre sempre que um objeto de sequência recebe uma solicitação para gerar o próximo valor para a opção **CACHE**, quando o cache está esgotado:  
  
1.  O próximo valor para o objeto de sequência é calculado.  
  
2.  O último valor para o novo cache é calculado.  
  
3.  A linha da tabela do sistema para o objeto de sequência está bloqueada, e o valor calculado na etapa 2 (o último valor) é gravado na tabela do sistema. Um xevent de cache esgotado é disparado para notificar o usuário sobre o novo valor contínuo.  
  
**Opção NO CACHE**  
  
 O processo a seguir ocorre sempre que um objeto de sequência recebe uma solicitação para gerar o próximo valor para a opção **NO CACHE**:  
  
1.  O próximo valor para o objeto de sequência é calculado.  
  
2.  O novo valor atual para o objeto de sequência é gravado na tabela do sistema.  
  
3.  O valor calculado é retornado à instrução de chamada.  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre sequências, consulte [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão **CREATE SEQUENCE**, **ALTER**ou **CONTROL** no SCHEMA.  
  
-   Membros das funções de banco de dados fixas db_owner e db_ddladmin podem criar, alterar e remover objetos de sequência.  
  
-   Os membros das funções de banco de dados fixas db_owner e db_datawriter podem atualizar os objetos de sequência fazendo com que gerem números.  
  
 O exemplo a seguir concede ao usuário permissão AdventureWorks\Larry criar sequências no esquema de teste.  
  
```sql  
GRANT CREATE SEQUENCE ON SCHEMA::Test TO [AdventureWorks\Larry]  
```  
  
 A propriedade de um objeto de sequência pode ser transferida usando a instrução **ALTER AUTHORIZATION**.  
  
 Se uma sequência utilizar um tipo de dados definido pelo usuário, o autor da sequência deverá ter a permissão REFERENCES nesse tipo.  
  
### <a name="audit"></a>Audit  
 Para auditar **CREATE SEQUENCE**, monitore o **SCHEMA_OBJECT_CHANGE_GROUP**.  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos de como criar sequências e usar a função **NEXT VALUE FOR** para gerar números de sequência, veja [Números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 A maioria dos exemplos a seguir cria objetos de sequência em um esquema denominado Teste.  
  
 Para criar o esquema de Teste, execute a instrução a seguir.  
  
```sql  
CREATE SCHEMA Test ;  
GO  
```  
  
### <a name="a-creating-a-sequence-that-increases-by-1"></a>a. Criando uma sequência que aumenta em 1  
 No exemplo a seguir, Thierry cria uma sequência chamada CountBy1, que aumenta em incrementos de um cada vez que é utilizada.  
  
```sql  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="b-creating-a-sequence-that-decreases-by-1"></a>B. Criando uma sequência que diminui em 1  
 O exemplo a seguir inicia em 0 e conta em decrementos negativos de um cada vez que é usada.  
  
```sql  
CREATE SEQUENCE Test.CountByNeg1  
    START WITH 0  
    INCREMENT BY -1 ;  
GO  
```  
  
### <a name="c-creating-a-sequence-that-increases-by-5"></a>C. Criando uma sequência que aumenta em 5  
 O exemplo a seguir cria uma sequência que aumenta em incrementos de 5 cada vez que é utilizada.  
  
```sql  
CREATE SEQUENCE Test.CountBy1  
    START WITH 5  
    INCREMENT BY 5 ;  
GO  
```  
  
### <a name="d-creating-a-sequence-that-starts-with-a-designated-number"></a>D. Criando uma sequência que começa com um número designado  
 Depois de importar uma tabela, Thierry percebe que o número de ID mais alto usado é 24.328. Thierry precisa de uma sequência que gerará números que comecem em 24.329. O código a seguir cria uma sequência que inicia com 24.329 e incrementos de 1.  
  
```sql  
CREATE SEQUENCE Test.ID_Seq  
    START WITH 24329  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="e-creating-a-sequence-using-default-values"></a>E. Criando uma sequência usando valores padrão  
 O exemplo a seguir cria uma sequência que usa os valores padrão.  
  
```sql  
CREATE SEQUENCE Test.TestSequence ;  
```  
  
 Execute a instrução a seguir para exibir as propriedades da sequência.  
  
```sql  
SELECT * FROM sys.sequences WHERE name = 'TestSequence' ;  
```  
  
 Uma lista parcial da saída demonstra os valores padrão.  
  
| Saída | Valor padrão|  
|-|-|  
|`start_value`|`-9223372036854775808`|  
|`increment`|`1`|  
|`mimimum_value`|`-9223372036854775808`|  
|`maximum_value`|`9223372036854775807`|  
|`is_cycling`|`0`|  
|`is_cached`|`1`|  
|`current_value`|`-9223372036854775808`|  
  
### <a name="f-creating-a-sequence-with-a-specific-data-type"></a>F. Criando uma sequência com um tipo de dados específico

O exemplo a seguir cria uma sequência usando o tipo de dados **smallint**, com um intervalo de -32.768 a 32.767.  
  
```sql  
CREATE SEQUENCE SmallSeq 
    AS smallint ;  
```  
  
### <a name="g-creating-a-sequence-using-all-arguments"></a>G. Criando uma sequência com todos os argumentos  
 O exemplo a seguir cria uma sequência chamada DecSeq usando o tipo de dados **decimal**, com um intervalo de 0 a 255. A sequência começa com 125 e é incrementada em 25 sempre que um número é gerado. Como a sequência é configurada para executar um ciclo quando o valor excede o valor máximo de 200, a sequência é reiniciada no valor mínimo de 100.  
  
```sql  
CREATE SEQUENCE Test.DecSeq  
    AS decimal(3,0)   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
```  
  
 Execute a instrução a seguir para visualizar o primeiro valor; a opção `START WITH` de 125.  
  
```sql  
SELECT NEXT VALUE FOR Test.DecSeq;  
```  
  
 Execute a instrução mais três vezes para retornar 150, 175 e 200.  
  
 Execute a instrução novamente para saber como o valor inicial volta para a opção `MINVALUE` de 100.  
  
 Execute o código a seguir para confirmar o tamanho do cache e visualizar o valor atual.  
  
```sql  
SELECT cache_size, current_value   
FROM sys.sequences  
WHERE name = 'DecSeq' ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
