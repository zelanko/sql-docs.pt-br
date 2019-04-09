---
title: Guia de início rápido para uma execução de código "Hello World" básico R no T-SQL – SQL Server Machine Learning
description: Guia de início rápido para o script de R no SQL Server. Conheça os fundamentos de chamar o script de R usando o procedimento armazenado do sistema sp_execute_external_script um exercício de Olá, mundo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1c3ee703bca46bf46dba8225e1d28da3174dc932
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59240164"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>Início Rápido: Script de R "Hello world" no SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste início rápido, você aprenderá conceitos-chave, executando um "Hello World" R script inT-SQL, uma introdução para o **sp_execute_external_script** procedimento armazenado do sistema. 

## <a name="prerequisites"></a>Prerequisites

Um início rápido anterior, [R Verifique se existe no SQL Server](quickstart-r-verify.md), fornece informações e links para configurar o ambiente de R necessários para este início rápido.

## <a name="basic-r-interaction"></a>Interação de R básicos

Há duas maneiras que você pode executar código R no banco de dados SQL:

+ Adicionar script R como um argumento de procedimento armazenado do sistema, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).
+ De um [remoto R client](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client), conecte-se ao banco de dados SQL e executar o código usando o banco de dados SQL como o contexto de computação.

O exercício a seguir destina-se no modelo de interação de primeira: como passar o código R para um procedimento armazenado.

1. Execute um script simple para ver como um script R é executado no banco de dados SQL.

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'R',
    @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

2. Supondo que você tenha tudo o que configurar corretamente o resultado correto é calculado e o R `print` função retorna o resultado para o **mensagens** janela.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Ao obter **stdout** mensagens é útil ao testar seu código, mais geralmente, você precisa retornar os resultados em formato tabular, para que você possa usá-lo em um aplicativo ou escrevê-lo a uma tabela. Consulte [guia de início rápido: Identificador de entradas e saídas usando o R no SQL Server](rtsql-working-with-inputs-and-outputs.md) para obter mais informações.

Lembre-se de tudo dentro de `@script` argumento deve ser um código R válido.

## <a name="run-a-hello-world-script"></a>Executar um script Hello World

O exercício a seguir executa outro scripts simples do R.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

Entradas para esse procedimento armazenado incluem:

+ *@language* parâmetro define a extensão da linguagem para chamar, nesse caso, R.
+ *@script* o parâmetro define os comandos transmitidos para o tempo de execução de R. Todo o script R deve ser colocado neste argumento, como texto Unicode. Você também pode adicionar texto a uma variável do tipo **nvarchar** e chamar a variável.
+ *@input_data_1* dados são retornados pela consulta, passada para o tempo de execução de R, que retorna os dados para o SQL Server como um quadro de dados.
+ COM conjuntos de resultados cláusula define o esquema da tabela de dados retornados para o SQL Server, adicionando "Hello World" como o nome da coluna **int** para o tipo de dados.

**Resultados**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>Próximas etapas

Agora que executar alguns scripts de R simples, dar uma olhada nas estruturação de entradas e saídas.

> [!div class="nextstepaction"]
> [Início Rápido: Lidar com entradas e saídas](quickstart-r-inputs-and-outputs.md)
