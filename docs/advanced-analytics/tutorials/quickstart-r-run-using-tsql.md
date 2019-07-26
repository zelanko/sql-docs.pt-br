---
title: Início rápido para uma execução de código R básica "Olá, Mundo" no T-SQL
description: Início rápido para script R no SQL Server. Aprenda as noções básicas de chamar o script R usando o procedimento armazenado do sistema sp_execute_external_script em um exercício de Olá, mundo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: ab73e0231f462504652e0e1af62fed80c706f061
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469032"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>Início Rápido: Script R "Olá mundo" no SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste guia de início rápido, você aprende os principais conceitos executando um "Olá, Mundo" script R inT-SQL, com uma introdução ao procedimento armazenado do sistema **sp_execute_external_script** . 

## <a name="prerequisites"></a>Pré-requisitos

Um guia de início rápido anterior, [verificar se o R existe no SQL Server](quickstart-r-verify.md), fornece informações e links para configurar o ambiente de R necessário para este guia de início rápido.

## <a name="basic-r-interaction"></a>Interação básica com o R

Há duas maneiras de executar o código R no banco de dados SQL:

+ Adicione o script R como um argumento do procedimento armazenado do sistema, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).
+ De um [cliente R remoto](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client), conecte-se ao banco de dados SQL e execute o código usando o banco de dados SQL como o contexto de computação.

O exercício a seguir concentra-se no primeiro modelo de interação: como transmitir código R para um procedimento armazenado.

1. Execute um script simples para ver como um script R é executado no banco de dados SQL.

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

2. Supondo que tudo esteja configurado corretamente, o resultado correto é calculado e a função R `print` retorna o resultado para a janela **mensagens** .

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Embora a obtenção de mensagens **stdout** seja útil ao testar seu código, com mais frequência você precisa retornar os resultados em formato tabular, para que você possa usá-lo em um aplicativo ou gravá-lo em uma tabela. Consulte [início rápido: Manipule entradas e saídas usando o R no](rtsql-working-with-inputs-and-outputs.md) SQL Server para obter mais informações.

Lembre-se de que `@script` tudo dentro do argumento deve ser um código R válido.

## <a name="run-a-hello-world-script"></a>Executar um script de Olá, Mundo

O exercício a seguir executa outros scripts R simples.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

As entradas para esse procedimento armazenado incluem:

+ *@language* define a extensão de linguagem a ser chamada, neste caso, R.
+ *@script* define os comandos passados para o tempo de execução de R. Todo o script R deve ser colocado neste argumento, como texto Unicode. Você também pode adicionar texto a uma variável do tipo **nvarchar** e chamar a variável.
+ *@input_data_1* são dados retornados pela consulta, passados para o tempo de execução de R, que retorna os dados para SQL Server como um quadro de dados.
+ COM a cláusula de conjuntos de resultados define o esquema da tabela de dados retornada para SQL Server, adicionando "Olá, Mundo" como o nome da coluna, **int** para o tipo de dados.

**Resultados**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>Próximas etapas

Agora que você executou alguns scripts R simples, dê uma olhada em mais detalhes na estrutura de entradas e saídas.

> [!div class="nextstepaction"]
> [Início Rápido: Manipular entradas e saídas](quickstart-r-inputs-and-outputs.md)
