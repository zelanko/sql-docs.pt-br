---
title: "CRIAR a SEQUÊNCIA (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 40
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 89a96d101c17f528b9ff14ca523e5dc41ada2f4c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-sequence-transact-sql"></a>CREATE SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Cria um objeto de sequência e especifica suas propriedades. Uma sequência é um objeto associado a um esquema definido pelo usuário que gera uma sequência de valores numéricos de acordo com a especificação com a qual a sequência foi criada. A sequência de valores numéricos é gerada em ordem crescente ou decrescente em um intervalo definido e pode ser configurada para reiniciar (em um ciclo) quando se esgotar. As sequências, ao contrário de colunas de identidade, não são associadas a tabelas específicas. Os aplicativos fazem referência a um objeto de sequência para recuperar seu próximo valor. A relação entre sequências e tabelas é controlada pelo aplicativo. Os aplicativos de usuário podem referenciar um objeto de sequência e coordenar os valores nas várias linhas e tabelas.  
  
 Ao contrário de valores de colunas de identidade que são gerados quando linhas são inseridas, um aplicativo pode obter o próximo número de sequência sem inserir a linha chamando o [função NEXT VALUE FOR](../../t-sql/functions/next-value-for-transact-sql.md). Use [sp_sequence_get_range](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md) para obter vários números de sequência de uma vez.  
  
 Para obter informações e cenários que usam **CREATE SEQUENCE** e a função **NEXT VALUE FOR** , consulte [Números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
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
  
## <a name="arguments"></a>Argumentos  
 *sequence_name*  
 Especifica o nome exclusivo pelo qual a sequência é conhecida no banco de dados. O tipo é **sysname**.  
  
 [ built_in_integer_type | user-defined_integer_type  
 Uma sequência pode ser definida como qualquer tipo de inteiro. Os seguintes tipos são permitidos:  
  
-   **tinyint** -intervalo de 0 a 255.  
  
-   **smallint** -intervalo de -32.768 a 32.767  
  
-   **int** -intervalo de -2.147.483.648 a 2.147.483.647  
  
-   **bigint** -intervalo 9.223.372.036.854.775.808 a 9.223.372.036.854.775.807.  
  
-   **decimal** e **numérico** com uma escala de 0.  
  
-   Qualquer tipo de dados definido pelo usuário (tipo de alias) que seja baseado em um dos tipos permitidos.  
  
 Se nenhum tipo de dados for fornecido, o **bigint** tipo de dados é usado como o padrão.  
  
 Iniciar com \<constante >  
 O primeiro valor retornado pelo objeto de sequência. O **iniciar** valor deve ser um valor menor ou igual ao máximo e maior ou igual ao valor mínimo do objeto de sequência. O valor de início padrão para um novo objeto de sequência é o valor mínimo para um objeto de sequência e o valor máximo de um objeto de sequência decrescente.  
  
 INCREMENT BY \<constante >  
 Valor usado para incrementar (ou decrementar, se negativo) o valor do objeto de sequência para cada chamada para o **NEXT VALUE FOR** função. Se o incremento for um valor negativo, o objeto de sequência será decrescente, caso contrário, será crescente. O incremento não pode ser 0. O incremento padrão para um novo objeto de sequência é 1.  
  
 [MINVALUE \<constante > | **Nenhum MINVALUE** ]  
 Especifica os limites do objeto de sequência. O valor mínimo padrão de um novo objeto de sequência é o valor mínimo do tipo de dados do objeto de sequência. É zero para o tipo de dados **tinyint** e um número negativo para todos os outros tipos de dados.  
  
 [MAXVALUE \<constante > | **Nenhum MAXVALUE**  
 Especifica os limites do objeto de sequência. O valor máximo padrão para um novo objeto de sequência é o valor máximo do tipo de dados do objeto de sequência.  
  
 [CICLO | **NENHUM CICLO** ]  
 Propriedade que especifica se o objeto de sequência deve reiniciar do valor mínimo (ou máximo para objetos de sequência decrescente) ou deve lançar uma exceção quando seu valor mínimo ou máximo é excedido. A opção de ciclo padrão para novos objetos de sequência é NO CYCLE.  
  
 Observe que o ciclo é reiniciado a partir do valor mínimo ou máximo, não do valor inicial.  
  
 [ **CACHE** [\<constante >] | NENHUM CACHE]  
 Aumenta o desempenho de aplicativos que usam objetos de sequência por meio da minimização do número de E/S de disco necessárias para gerar números de sequência. Padrões para o CACHE.  
  
 Por exemplo, se um tamanho de cache de 50 for escolhido, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não manterá 50 valores individuais em cache. Somente permanecem em cache o valor atual e o número de valores restantes no cache. Isso significa que a quantidade de memória necessária para armazenar o cache sempre é duas instâncias do tipo de dados do objeto de sequência.  
  
> [!NOTE]  
>  Se a opção de cache for habilitada sem a especificação de um tamanho de cache, o Mecanismo de Banco de Dados selecionará um tamanho. Porém, os usuários não devem confiar que a seleção será consistente. [!INCLUDE[msCoName](../../includes/msconame-md.md)] pode alterar o método de cálculo do tamanho do cache sem aviso prévio.  
  
 Quando criado com o **CACHE** , um desligamento inesperado (como uma falha de energia) pode resultar na perda de números de sequência restantes no cache.  
  
## <a name="general-remarks"></a>Comentários gerais  
 Os números de sequência são gerados fora do escopo da transação atual. Eles serão consumidos se a transação que usa o número de sequência for confirmada ou revertida.  
  
### <a name="cache-management"></a>Gerenciamento de cache  
 Para melhorar o desempenho, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pré-aloca o número de números de sequência especificados pelo **CACHE** argumento.  
  
 Por exemplo, uma nova sequência é criada com um valor inicial de 1 e um tamanho de cache de 15. Quando o primeiro valor é necessário, valores de 1 a 15 são disponibilizados da memória. O último valor em cache (15) é gravado nas tabelas do sistema no disco. Quando todos os 15 números são usados, a solicitação seguinte (pelo número 16) faz com que o cache seja alocado novamente. O novo valor colocado no cache por último (30) será gravado nas tabelas do sistema.  
  
 Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for interrompido depois que você usar 22 números, o próximo número de sequência pretendido na memória (23) será gravado nas tabelas do sistema, substituindo o número armazenado antes.  
  
 Após a reinicialização do SQL Server e quando um número de sequência for necessário, o número inicial será lido nas tabelas do sistema (23). A quantidade de cache de 15 números (23-38) é alocada para a memória e o próximo número não de cache (39) é gravado nas tabelas do sistema.  
  
 Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para de modo anormal para um evento, como uma falha de energia, a sequência reiniciará com o número lido nas tabelas do sistema (39). Qualquer sequência de números alocados na memória (mas nunca solicitados por um usuário ou aplicativo) serão perdidos. Essa funcionalidade pode deixar intervalos, mas garante que o mesmo valor nunca será emitido duas vezes para um único objeto de sequência, a menos que ele está definido como **ciclo** ou reiniciado manualmente.  
  
 O cache é mantido na memória por meio do acompanhamento do valor atual (o último valor emitido) e o número de valores restantes no cache. Portanto, a quantidade de memória usada pelo cache sempre é duas instâncias do tipo de dados do objeto de sequência.  
  
 A definição do argumento de cache **NO CACHE** grava o valor de sequência atual nas tabelas do sistema toda vez que uma sequência é usada. Isso pode prejudicar o desempenho ao aumentar o acesso ao disco, mas reduz a possibilidade de intervalos não intencionais. Ainda poderão ocorrer intervalos se os números forem solicitados usando o **NEXT VALUE FOR** ou **sp_sequence_get_range** funções, mas, em seguida, os números não são usados ou são usadas em transações não confirmadas.  
  
 Quando um objeto de sequência usa o **CACHE** opção, se você reiniciar o objeto de sequência, ou alterar o **INCREMENTO**, **ciclo**, **MINVALUE**, **MAXVALUE**, ou as propriedades de tamanho do cache, ela fará com que o cache seja gravado nas tabelas do sistema antes da alteração. Em seguida, o cache é recarregado a partir do valor atual (ou seja, nenhum número é ignorado). A alteração do tamanho do cache entra em vigor imediatamente.  
  
 **Opção CACHE quando os valores armazenados em cache estão disponíveis**  
  
 O seguinte processo ocorre sempre que um objeto de sequência é solicitado para gerar o próximo valor para o **CACHE** opção se houver valores não usados disponíveis no cache de memória para o objeto de sequência.  
  
1.  O próximo valor para o objeto de sequência é calculado.  
  
2.  O novo valor atual para o objeto de sequência é atualizado na memória.  
  
3.  O valor calculado é retornado à instrução de chamada.  
  
 **Opção de CACHE quando o cache está esgotado**  
  
 O seguinte processo ocorre sempre que um objeto de sequência é solicitado para gerar o próximo valor para o **CACHE** opção se o cache está esgotado:  
  
1.  O próximo valor para o objeto de sequência é calculado.  
  
2.  O último valor para o novo cache é calculado.  
  
3.  A linha da tabela do sistema para o objeto de sequência está bloqueada, e o valor calculado na etapa 2 (o último valor) é gravado na tabela do sistema. Um xevent de cache esgotado é disparado para notificar o usuário sobre o novo valor contínuo.  
  
 **NENHUMA opção de CACHE**  
  
 O seguinte processo ocorre sempre que um objeto de sequência é solicitado para gerar o próximo valor para o **NO CACHE** opção:  
  
1.  O próximo valor para o objeto de sequência é calculado.  
  
2.  O novo valor atual para o objeto de sequência é gravado na tabela do sistema.  
  
3.  O valor calculado é retornado à instrução de chamada.  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre sequências, consulte [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão **CREATE SEQUENCE**, **ALTER**ou **CONTROL** no SCHEMA.  
  
-   Membros de db_owner e db_ddladmin banco de dados fixa podem criar, alterar e remover objetos de sequência.  
  
-   Membros de db_owner e db_datawriter banco de dados fixa podem atualizar objetos de sequência fazendo com que a geração de números.  
  
 O exemplo a seguir concede ao usuário permissão AdventureWorks\Larry criar sequências no esquema de teste.  
  
```  
GRANT CREATE SEQUENCE ON SCHEMA::Test TO [AdventureWorks\Larry]  
```  
  
 Propriedade de um objeto de sequência pode ser transferida usando o **ALTER AUTHORIZATION** instrução.  
  
 Se uma sequência utilizar um tipo de dados definido pelo usuário, o autor da sequência deverá ter a permissão REFERENCES nesse tipo.  
  
### <a name="audit"></a>Auditoria  
 Para auditar **CREATE SEQUENCE**, monitor de **SCHEMA_OBJECT_CHANGE_GROUP**.  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos de como criar sequências e usar o **NEXT VALUE FOR** função para gerar números de sequência, consulte [números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 A maioria dos exemplos a seguir cria objetos de sequência em um esquema denominado Test.  
  
 Para criar o esquema de teste, execute a seguinte instrução.  
  
```  
CREATE SCHEMA Test ;  
GO  
```  
  
### <a name="a-creating-a-sequence-that-increases-by-1"></a>A. Criando uma sequência que aumenta em 1  
 No exemplo a seguir, Thierry cria uma sequência denominada CountBy1 que aumenta em um toda vez que ela é usada.  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 1  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="b-creating-a-sequence-that-decreases-by-1"></a>B. Criando uma sequência que diminui em 1  
 O exemplo a seguir inicia em 0 e conta em decrementos negativos de um cada vez que é usada.  
  
```  
CREATE SEQUENCE Test.CountByNeg1  
    START WITH 0  
    INCREMENT BY -1 ;  
GO  
```  
  
### <a name="c-creating-a-sequence-that-increases-by-5"></a>C. Criando uma sequência que aumenta em 5  
 O exemplo a seguir cria uma sequência que aumenta em incrementos de 5 cada vez que é utilizada.  
  
```  
CREATE SEQUENCE Test.CountBy1  
    START WITH 5  
    INCREMENT BY 5 ;  
GO  
```  
  
### <a name="d-creating-a-sequence-that-starts-with-a-designated-number"></a>D. Criando uma sequência que começa com um número designado  
 Depois de importar uma tabela, Thierry percebe que o número de ID mais alto usado é 24.328. Thierry precisa de uma sequência que gerará números que comecem em 24.329. O código a seguir cria uma sequência que inicia com 24.329 e incrementos de 1.  
  
```  
CREATE SEQUENCE Test.ID_Seq  
    START WITH 24329  
    INCREMENT BY 1 ;  
GO  
```  
  
### <a name="e-creating-a-sequence-using-default-values"></a>E. Criando uma sequência usando valores padrão  
 O exemplo a seguir cria uma sequência que usa os valores padrão.  
  
```  
CREATE SEQUENCE Test.TestSequence ;  
```  
  
 Execute a instrução a seguir para exibir as propriedades da sequência.  
  
```  
SELECT * FROM sys.sequences WHERE name = 'TestSequence' ;  
```  
  
 Uma lista parcial da saída demonstra os valores padrão.  
  
|||  
|-|-|  
|`start_value`|`-9223372036854775808`|  
|`increment`|`1`|  
|`mimimum_value`|`-9223372036854775808`|  
|`maximum_value`|`9223372036854775807`|  
|`is_cycling`|`0`|  
|`is_cached`|`1`|  
|`current_value`|`-9223372036854775808`|  
  
### <a name="f-creating-a-sequence-with-a-specific-data-type"></a>F. Criando uma sequência com um tipo de dados específico  
 O exemplo a seguir cria uma sequência usando o **smallint** tipo de dados, com um intervalo de -32.768 a 32.767.  
  
```  
CREATE SEQUENCE SmallSeq  
    AS smallint ;  
```  
  
### <a name="g-creating-a-sequence-using-all-arguments"></a>G. Criando uma sequência com todos os argumentos  
 O exemplo a seguir cria uma sequência chamada DecSeq usando o **decimal** tipo de dados, com um intervalo de 0 a 255. A sequência começa com 125 e é incrementada em 25 sempre que um número é gerado. Como a sequência é configurada para executar um ciclo quando o valor excede o valor máximo de 200, a sequência é reiniciada no valor mínimo de 100.  
  
```  
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
  
```  
SELECT NEXT VALUE FOR Test.DecSeq;  
```  
  
 Execute a instrução mais três vezes para retornar 150, 175 e 200.  
  
 Execute a instrução novamente para saber como o valor inicial volta para a opção `MINVALUE` de 100.  
  
 Execute o código a seguir para confirmar o tamanho do cache e visualizar o valor atual.  
  
```  
SELECT cache_size, current_value   
FROM sys.sequences  
WHERE name = 'DecSeq' ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER SEQUENCE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [PRÓXIMO valor para &#40; Transact-SQL &#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  

