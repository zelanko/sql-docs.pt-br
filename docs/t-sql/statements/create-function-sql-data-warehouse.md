---
title: "Criar função (SQL Data Warehouse) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8cad1b2c-5ea0-4001-9060-2f6832ccd057
caps.latest.revision: 14
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 55f1b7e612a1c7d120e06078b0fdba45d6409d36
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-function-sql-data-warehouse"></a>Criar função (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Cria uma função definida pelo usuário no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]. Uma função definida pelo usuário é um [!INCLUDE[tsql](../../includes/tsql-md.md)] rotina que aceita parâmetros, executa uma ação, como um cálculo complexo e retorna o resultado dessa ação como um valor. O valor de retorno deve ser um valor escalar (único). Use essa instrução para criar uma rotina reutilizável que possa ser usada destas maneiras:  
  
-   Em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)], como SELECT  
  
-   Em aplicativos que chamam a função  
  
-   Na definição de outra função definida pelo usuário  
  
-   Para definir uma restrição CHECK em uma coluna  
  
-   Para substituir um procedimento armazenado  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
--Transact-SQL Scalar Function Syntax  
CREATE FUNCTION [ schema_name. ] function_name   
( [ { @parameter_name [ AS ] parameter_data_type   
    [ = default ] }   
    [ ,...n ]  
  ]  
)  
RETURNS return_data_type  
    [ WITH <function_option> [ ,...n ] ]  
    [ AS ]  
    BEGIN   
        function_body   
        RETURN scalar_expression  
    END  
[ ; ]  
  
<function_option>::=   
{  
    [ SCHEMABINDING ]  
  | [ RETURNS NULL ON NULL INPUT | CALLED ON NULL INPUT ]  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *schema_name*  
 É o nome do esquema ao qual a função definida pelo usuário pertence.  
  
 *nome_da_função*  
 É o nome da função definida pelo usuário. Nomes de função devem estar de acordo com as regras para identificadores e devem ser exclusivos no banco de dados e seu esquema.  
  
> [!NOTE]  
>  São necessários parênteses depois do nome de função mesmo que um parâmetro não seja especificado.  
  
 @*parameter_name*  
 É um parâmetro na função definida pelo usuário. Podem ser declarados um ou mais parâmetros.  
  
 Uma função pode ter no máximo 2.100 parâmetros. O valor de cada parâmetro declarado deve ser fornecido pelo usuário quando a função é executada, a menos que seja definido um padrão para o parâmetro.  
  
 Especifique um nome de parâmetro usando um sinal de arroba (@) como o primeiro caractere. O nome do parâmetro deve estar em conformidade com as regras de identificadores. Os parâmetros são locais para a função. Os mesmos nomes de parâmetro podem ser usados em outras funções. Os parâmetros só podem assumir o lugar de constantes. Eles não podem ser usados no lugar de nomes de tabela, nomes de coluna ou nomes de outros objetos de banco de dados.  
  
> [!NOTE]  
>  ANSI_WARNINGS não é cumprido quando você passa parâmetros em um procedimento armazenado, em uma função definida pelo usuário ou quando declara ou define variáveis em uma instrução de lote. Por exemplo, se a variável é definida como **caractere (3)**e definido como um valor maior do que três caracteres, os dados são truncados para o tamanho definido e a inserção ou atualização instrução tem sucesso.  
  
 *parameter_data_type*  
 É o tipo de dados do parâmetro. Para [!INCLUDE[tsql](../../includes/tsql-md.md)] funções, todos os tipos de dados escalares com suporte no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] são permitidos. O tipo de dados de carimbo de hora (rowversion) não é um tipo com suporte.  
  
 [=*padrão* ]  
 É um valor padrão para o parâmetro. Se um *padrão* valor for definido, a função pode ser executada sem especificar um valor para esse parâmetro.  
  
 Quando um parâmetro da função tiver um valor padrão, a palavra-chave DEFAULT deverá ser especificada quando a função for chamada para recuperar o valor padrão. Esse comportamento é diferente do uso de parâmetros com valores padrão em procedimentos armazenados nos quais a omissão do parâmetro também indica o valor padrão.  
  
 *return_data_type*  
 É o valor de retorno de uma função escalar definida pelo usuário. Para [!INCLUDE[tsql](../../includes/tsql-md.md)] funções, todos os tipos de dados escalares com suporte no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] são permitidos. O tipo de dados de carimbo de hora (rowversion) não é um tipo com suporte. Os tipos não escalares de cursor e a tabela não são permitidos.  
  
 *function_body*  
 Série de [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções.  O function_body não pode conter uma instrução SELECT e não pode fazer referência a dados do banco de dados.  O function_body não é possível fazer referência a tabelas ou exibições. O corpo da função pode chamar outras funções determinísticas, mas não é possível chamar funções não determinísticas. 
  
 Em funções escalares, *function_body* é uma série de [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções que juntas são avaliadas como um valor escalar.  
  
 *scalar_expression*  
 Especifica o valor escalar que a função escalar retorna.  
  
 **\<function_option >:: =** 
  
 Especifica que a função terá uma ou mais das opções a seguir.  
  
 SCHEMABINDING  
 Especifica que a função está associada aos objetos de banco de dados referenciados por ela. Quando SCHEMABINDING for especificado, os objetos base não poderão ser modificadas de um modo que possa afetar a definição da função. A própria definição da função deve ser primeiro modificada ou descartada para remover as dependências no objeto a ser modificado.  
  
 A associação da função aos objetos referenciados por ela será removida somente quando ocorrer uma das ações a seguir:  
  
-   A função for descartada.  
  
-   A função for modificada com o uso da instrução ALTER sem a especificação da opção SCHEMABINDING.  
  
 Uma função poderá ser associada a esquemas apenas se as condições a seguir forem verdadeiras:  
  
-   Quaisquer funções definidas pelo usuário referenciadas pela função são também associadas a esquema.  
  
-   As funções e outros UDFs referenciados pela função são referenciados usando um nome de parte única ou de duas partes.  
  
-   Somente funções internas e outros UDFs no mesmo banco de dados podem ser referenciados dentro do corpo de UDFs.  
  
-   O usuário que executou a instrução CREATE FUNCTION tem permissão REFERENCES nos objetos do banco de dados referidos pela função.  
  
 Para remover SCHEMABINDING use ALTER  
  
 RETORNA NULL EM ENTRADA NULL | **CHAMADO EM ENTRADA NULL**  
 Especifica o **OnNULLCall** atributo de uma função com valor escalar. Se não for especificado, CALLED ON NULL INPUT será implícito por padrão. Isso significa que o corpo da função será executado mesmo que NULL seja passado como um argumento.  
  
## <a name="best-practices"></a>Práticas recomendadas  
 Se uma função definida pelo usuário não for criada com a cláusula SCHEMABINDING, as alterações feitas nos objetos subjacentes poderão afetar a definição da função e produzir resultados inesperados quando ela for chamada. É recomendável que você implemente um dos seguintes métodos para garantir que a função não se torne desatualizada devido a alterações em seus objetos subjacentes:  
  
-   Especifique a cláusula WITH SCHEMABINDING quando estiver criando a função. Isso garante que os objetos referenciados na definição da função não possam ser modificados, a menos que a função também seja modificada.  
  
## <a name="interoperability"></a>Interoperabilidade  
 As instruções a seguir são válidas em uma função:  
  
-   Instruções de atribuição.  
  
-   Instruções de controle de fluxo com exceção das instruções TRY...CATCH.  
  
-   Instruções DECLARE que definem variáveis de dados local.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Funções definidas pelo usuário não podem ser usadas para executar ações que modificam o estado do banco de dados.  
  
 Funções definidas pelo usuário podem ser aninhadas, isto é, uma função definida pelo usuário pode chamar outra. O nível de aninhamento é incrementado quando a execução da função é iniciada, e reduzido quando a execução da função chamada é concluída. Até 32 níveis de funções definidas pelo usuário podem ser aninhados. Se o máximo de níveis de aninhamento for excedido haverá falha em toda a cadeia de funções da chamada de aninhamento.   
  
## <a name="metadata"></a>Metadados  
 Esta seção lista as exibições de catálogo do sistema que você pode usar para retornar metadados sobre funções definidas pelo usuário.  
  
 [sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) : exibe a definição de [!INCLUDE[tsql](../../includes/tsql-md.md)] funções definidas pelo usuário. Por exemplo:  
  
```  
SELECT definition, type   
FROM sys.sql_modules AS m  
JOIN sys.objects AS o   
    ON m.object_id = o.object_id   
    AND type = ('FN');  
GO  
  
```  
  
 [sys. Parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md) : exibe informações sobre os parâmetros definidos em funções definidas pelo usuário.  
  
 [sys. sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) : exibe os objetos subjacentes referenciados por uma função.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão CREATE FUNCTION no banco de dados e a permissão ALTER no esquema no qual a função está sendo criada.  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-a-scalar-valued-user-defined-function-to-change-a-data-type"></a>A. Usando uma função com valor escalar definida pelo usuário para alterar um tipo de dados  
 Essa função simple usa uma **int** de tipo de dados como uma entrada e retorna um **decimal(10,2)** tipo de dados como uma saída.  
  
```  
CREATE FUNCTION dbo.ConvertInput (@MyValueIn int)  
RETURNS decimal(10,2)  
AS  
BEGIN  
    DECLARE @MyValueOut int;  
    SET @MyValueOut= CAST( @MyValueIn AS decimal(10,2));  
    RETURN(@MyValueOut);  
END;  
GO  
  
SELECT dbo.ConvertInput(15) AS 'ConvertedValue';  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER FUNCTION (SQL Server PDW)](http://msdn.microsoft.com/en-us/25ff3798-eb54-4516-9973-d8f707a13f6c)   
 [Remover função (SQL Server PDW)](http://msdn.microsoft.com/en-us/1792a90d-0d06-4852-9dec-6de1b9cd229e)  
  
  



