---
title: Trabalhando com entradas e saídas (R no início rápido do SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 831ca196f4c45c169f398beb39895c7fa29e405f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="working-with-inputs-and-outputs-r-in-sql-quickstart"></a>Trabalhando com entradas e saídas (R no início rápido do SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Quando você quiser executar o código R no SQL Server, você deve encapsular o script R em um procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Esse procedimento armazenado é usado para iniciar o tempo de execução de R no contexto do SQL Server, que transmite dados para R, gerencia as sessões de usuário de R com segurança e retorna todos os resultados para o cliente.

## <a name="bkmk_SSMSBasics"></a>Criar alguns dados de teste simples

Crie uma pequena tabela de dados de teste executando a seguinte instrução T-SQL:

```sql
CREATE TABLE RTestData ([col1] int not null) ON [PRIMARY]
INSERT INTO RTestData   VALUES (1);
INSERT INTO RTestData   VALUES (10);
INSERT INTO RTestData   VALUES (100) ;
GO
```

Assim que a tabela tiver sido criada, use a seguinte instrução para consultar a tabela:
  
```sql
SELECT * FROM RTestData
```

**Resultados**

|col1|
|------|
|*1*|
|*10*|
|*100*|

## <a name="get-the-same-data-using-r-script"></a>Obter os mesmos dados usando script R

Depois que a tabela for criada, execute a seguinte instrução:

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N' OutputDataSet <- InputDataSet;'
    , @input_data_1 = N' SELECT *  FROM RTestData;'
    WITH RESULT SETS (([NewColName] int NOT NULL));
```

Obtém os dados da tabela, faz uma viagem de ida e pelo tempo de execução de R e retorna os valores com o nome da coluna *NewColName*.

**Resultados**

![rsql_basictut_getsamedataR](media/rsql-basictut-getsamedatar.PNG)


**Comentários**

+ No Management Studio, resultados tabulares são retornados no painel **Valores**. As mensagens retornadas pelo tempo de execução do R são apresentadas no painel **Mensagens**.
+ O parâmetro *@language* define a extensão da linguagem a ser chamada, neste caso, R.
+ No parâmetro *@script*, você define os comandos a passar ao tempo de execução de R. Todo o script R deve ser colocado neste argumento, como texto Unicode. Você também pode adicionar texto a uma variável do tipo **nvarchar** e chamar a variável.
+ Os dados retornados pela consulta são passados para o tempo de execução R, que retorna os dados ao SQL Server como um quadro de dados.
+ A cláusula WITH RESULT SETS define o esquema da tabela de dados retornada para o SQL Server.

## <a name="change-input-or-output-variables"></a>Alterar variáveis de entrada ou saída

O exemplo anterior usou os nomes de variável de entrada e saída padrão, _InputDataSet_ e _OutputDataSet_. Para definir os dados de entrada associados a _InputDatSet_, use a variável *@input_data_1*.

Neste exemplo, os nomes das variáveis de entrada e saída para o procedimento armazenado mudaram para *SQL_Out* e *SQL_In*:

```sql
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N' SQL_out <- SQL_in;'
  , @input_data_1 = N' SELECT 12 as Col;'
  , @input_data_1_name  = N'SQL_In'
  , @output_data_1_name =  N'SQL_Out'
  WITH RESULT SETS (([NewColName] int NOT NULL));
```

Você obteve o erro "objeto SQL\_no não encontrado"? Isso ocorre porque o R diferencia maiúsculas de minúsculas! No exemplo, o script R usa as variáveis *SQL_in* e *SQL_out*, mas os parâmetros para o procedimento armazenado usam as variáveis *SQL_In* e *SQL_Out*.

Isso ocorre porque o R diferencia maiusculas de minúsculas. No exemplo, o script R usa as variáveis *SQL_in* e *SQL_out*, mas os parâmetros para o procedimento armazenado usam as variáveis *SQL_In* e *SQL_Out*.
Tente corrigir **somente** o *SQL_In* variável e execute novamente o procedimento armazenado.

Agora que você obtenha uma **diferentes** erro:

```Error
EXECUTE statement failed because its WITH RESULT SETS clause specified 1 result set(s), but the statement only sent 0 result set(s) at run time.
```

Estamos mostrando você esse erro porque você pode esperar para vê-lo, geralmente, ao testar o novo código de R. Isso significa que o script R foi executado com êxito, mas do SQL Server não recebeu nenhum dado ou recebeu dados incorreto ou inesperados.

Nesse caso, o esquema de saída (a linha que começa com **WITH**) especifica que uma coluna de dados de inteiros deve ser retornada, porém, considerando que R coloca os dados em uma variável diferente, nada voltou ao SQL Server; assim, ocorreu o erro. Para corrigir o erro, corrija o segundo nome de variável.

**Lembre-se esses requisitos!**

- Nomes de variáveis devem seguir as regras para identificadores SQL válidos.
- A ordem dos parâmetros é importante. Você deve especificar os parâmetros necessários *@input_data_1* e *@output_data_1* primeiro para usar os parâmetros opcionais *@input_data_1_name* e *@output_data_1_name*.
- Apenas um conjunto de dados de entrada pode ser passado como um parâmetro e é possível retornar apenas um conjunto de dados. No entanto, você pode chamar outros conjuntos de dados no código do R e retornar saídas de outros tipos, além do conjunto de dados. Você também pode adicionar a palavra-chave OUTPUT a qualquer parâmetro para que ele seja retornado com os resultados. Há um exemplo simples mais adiante neste tutorial.
- A instrução `WITH RESULT SETS` define o esquema de dados em prol do SQL Server. Você precisa fornecer tipos de dados compatíveis do SQL para cada coluna retornada do R. Use a definição de esquema para fornecer novos nomes de coluna. Não é preciso usar os nomes de coluna do R data.frame. Em alguns casos, essa cláusula é opcional. Tente omiti-lo e ver o que acontece.

## <a name="generate-results-using-r"></a>Gerar resultados usando o R

Você também pode gerar valores usando apenas o script R e deixar a cadeia de caracteres de consulta de entrada em _@input_data_1_ em branco. Ou usar uma instrução SQL SELECT válida como um espaço reservado e não usar os resultados do SQL no script R.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
   , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
   , @input_data_1 = N' SELECT 1 as Temp1'
   WITH RESULT SETS (([Col1] char(20) NOT NULL));
```

**Resultados**

*Col1*
*hello*
<code>   </code>
*world*

## <a name="next-lesson"></a>Próxima lição

Você examinará alguns dos problemas que podem ser encontrados ao passar dados entre R e SQL Server, como conversões implícitas e diferenças em dados tabulares entre R e SQL.

[Tipo de dados SQL e R e objetos de dados](../tutorials/rtsql-r-and-sql-data-types-and-data-objects.md)
