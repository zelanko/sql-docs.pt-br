---
title: 'Início Rápido: Python "Olá, Mundo"'
description: Neste guia de início rápido, você aprende os principais conceitos executando um script Python "Olá, Mundo" em SQL Server Serviços de Machine Learning. Você usará o procedimento armazenado do sistema sp_execute_external_script T-SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1149c7888bc783c9d4f658eed5e8405214d6ffc4
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69530973"
---
# <a name="quickstart-run-a-hello-world-python-script-on-sql-server-machine-learning-services"></a>Início Rápido: Execute um script Python "Olá, mundo" em SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste guia de início rápido, você aprende os principais conceitos executando um script Python "Olá, Mundo" em SQL Server Serviços de Machine Learning. Você usará o procedimento armazenado do sistema **Sp_execute_external_script** T-SQL.

## <a name="prerequisites"></a>Pré-requisitos

Um guia de início rápido anterior, [Verifique se o Python existe no SQL Server](quickstart-python-verify.md), fornece informações e links para configurar o ambiente do Python necessário para este guia de início rápido.

## <a name="basic-python-interaction"></a>Interação básica com o Python

Há duas maneiras de executar o código Python no SQL Server:

+ Adicione um script Python como um argumento do procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ De um [cliente Python remoto](../python/setup-python-client-tools-sql.md), conecte-se a SQL Server e execute o código usando o SQL Server como o contexto de computação. Isso requer [revoscalepy](../python/ref-py-revoscalepy.md).

O exercício a seguir concentra-se no primeiro modelo de interação: como passar o código Python para um procedimento armazenado.

1. Execute um código simples para ver como os dados são passados para frente e para trás entre SQL Server e Python.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. Supondo que você tenha tudo configurado corretamente, e Python e SQL Server estão se comunicando entre si, o resultado correto é calculado e a função `print` Python retorna o resultado para as janelas de **mensagens** .

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    Embora a obtenção de mensagens **stdout** seja útil ao testar seu código, com mais frequência você precisa retornar os resultados em formato tabular, para que você possa usá-lo em um aplicativo ou gravá-lo em uma tabela.

Por enquanto, lembre-se destas regras:

+ Tudo dentro do `@script` argumento deve ser um código Python válido. 
+ O código deve seguir todas as regras do Python sobre recuo, nomes de variáveis e assim por diante. Quando receber um erro, verifique seu espaço em branco e maiúsculas e minúsculas.
+ Entre linguagens de programação, o Python é um dos mais flexíveis em relação a aspas simples versus aspas duplas; Eles são muito intercambiáveis. No entanto, o T-SQL usa aspas simples apenas para determinadas coisas `@script` , e o argumento usa aspas simples para colocar o código Python como uma cadeia de caracteres Unicode. Portanto, talvez seja necessário revisar seu código Python e alterar algumas aspas simples para aspas duplas.
+ Se você estiver usando bibliotecas que não são carregadas por padrão, deverá usar uma instrução de importação no início do script para carregá-las. SQL Server adiciona várias bibliotecas específicas do produto. Para obter mais informações, consulte [bibliotecas do Python](../python/python-libraries-and-data-types.md).
+ Se a biblioteca ainda não estiver instalada, pare e instale o pacote do Python fora do SQL Server, conforme descrito aqui: [Instalar os novos pacotes Python no SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>Executar um script de Olá, Mundo

O exercício a seguir executa outros scripts simples do Python.

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

As entradas para esse procedimento armazenado incluem:

+ *@language* define a extensão de linguagem a ser chamada, nesse caso, Python.
+ *@script* define os comandos passados para o tempo de execução do Python. Todo o script do Python deve estar incluído nesse argumento, como texto Unicode. Você também pode adicionar texto a uma variável do tipo **nvarchar** e chamar a variável.
+ *@input_data_1* são dados retornados pela consulta, passados para o tempo de execução do Python, que retorna os dados para SQL Server como um quadro de dados.
+ COM a cláusula de conjuntos de resultados define o esquema da tabela de dados retornada para SQL Server, adicionando "Olá, Mundo" como o nome da coluna, **int** para o tipo de dados.

**Resultados**

| Hello World |
|-------------|
| 1 |

## <a name="next-steps"></a>Próximas etapas

Agora que você executou alguns scripts Python simples, dê uma olhada em mais detalhes na estrutura de entradas e saídas.

> [!div class="nextstepaction"]
> [Início Rápido: Manipular entradas e saídas](quickstart-python-inputs-and-outputs.md)
