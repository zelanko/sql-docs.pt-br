---
title: Converter código R para procedimentos armazenados
description: Migre o código R para um procedimento armazenado SQL Server para implantação de solução e acesso a dados para dados relacionais no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: a2bd6db3aaae2c07f6f46aecce3e7df913fc2a9e
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470244"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>Converter código R para execução em instâncias SQL Server (no banco de dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo fornece diretrizes de alto nível sobre como modificar o código R para trabalhar em SQL Server. 

Quando você move o código R do R Studio ou outro ambiente para SQL Server, geralmente o código funciona sem modificação adicional: por exemplo, se o código for simples, como uma função que usa algumas entradas e retorna um valor. Também é mais fácil de portar soluções que usam os pacotes **RevoScaleR** ou **MicrosoftML** , que dão suporte à execução em contextos de execução diferentes com alterações mínimas.

No entanto, seu código poderá exigir alterações substanciais se qualquer uma das seguintes opções for aplicável:

+ Você usa bibliotecas de R que acessam a rede ou que não podem ser instaladas em SQL Server.
+ O código faz chamadas separadas para fontes de dados fora SQL Server, como planilhas do Excel, arquivos em compartilhamentos e outros bancos de dado. 
+ Você deseja executar o código no *@script* parâmetro de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e também parametrizar o procedimento armazenado.
+ Sua solução original inclui várias etapas que podem ser mais eficientes em um ambiente de produção, se executadas de forma independente, como preparação de dados ou engenharia de recursos versus treinamento de modelo, pontuação ou relatório.
+ Você deseja melhorar a otimização do desempenho alterando as bibliotecas, usando a execução paralela ou descarregando algum processamento para SQL Server. 

## <a name="step-1-plan-requirements-and-resources"></a>Etapa 1. Requisitos e recursos do plano

**Pacotes**

+ Determine quais pacotes são necessários e certifique-se de que eles funcionem em SQL Server.
 
+ Instale pacotes com antecedência, na biblioteca de pacotes padrão usada pelo Serviços de Machine Learning. Não há suporte para bibliotecas de usuário.

**Fontes de dados** 

+ Se você pretende inserir o código R no [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identifique as fontes de dados primárias e secundárias. 

    + As fontes de dados **primárias** são grandes conjuntos de dados, como os de treinamento de modelo ou dados de entrada para previsões. Planeje mapear seu maior conjunto de dados para o parâmetro de entrada de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + As fontes de dados **secundárias** são normalmente conjuntos de dados menores, como listas de fatores ou variáveis de agrupamento adicionais. 
    
    Atualmente, o sp_execute_external_script dá suporte a apenas um único conjunto de dados como entrada para o procedimento armazenado. No entanto, você pode adicionar várias entradas escalares ou binárias.

    Chamadas de procedimento armazenado precedidas por EXECUTE não podem ser usadas como entrada para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Você pode usar consultas, exibições ou qualquer outra instrução SELECT válida.

+ Determine as saídas que você precisa. Se você executar o código R usando sp_execute_external_script, o procedimento armazenado poderá gerar apenas um quadro de dados como resultado. No entanto, você também pode gerar várias saídas escalares, incluindo plotagens e modelos em formato binário, bem como outros valores escalares derivados de código R ou parâmetros SQL.

**Tipos de dados**

+ Faça uma lista de verificação dos possíveis problemas de tipo de dados.

    Todos os tipos de dados do R são suportados por SQL Server serviços de Machine Learning. No entanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o oferece suporte a uma variedade maior de tipos de dados do que o R. Portanto, algumas conversões implícitas de tipo de dados são executadas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante o envio de dados para o R, e vice-versa. Talvez seja necessário converter explicitamente ou converter alguns dados. 

    Há suporte para valors NULL. No entanto, R `na` usa a construção de dados para representar um valor ausente, que é semelhante a um NULL.

+ Considere a eliminação de dependências de dados que não podem ser usados por R: por exemplo, os tipos de dados ROWID e GUID de SQL Server não podem ser consumidos por R e gerar erros.

    Para obter mais informações, consulte [bibliotecas e tipos de dados do R](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Etapa 2. Converter ou reempacotar código

O quanto você altera seu código depende se pretende enviar o código R de um cliente remoto para ser executado no contexto de computação SQL Server ou pretende implantar o código como parte de um procedimento armazenado, o que pode fornecer melhor desempenho e segurança de dados. Encapsular seu código em um procedimento armazenado impõe alguns requisitos adicionais. 

+ Defina os dados de entrada primários como uma consulta SQL sempre que possível, para evitar a movimentação de dados.

+ Ao executar o R em um procedimento armazenado, você pode passar por  várias entradas escalares. Para todos os parâmetros que você deseja usar na saída, adicione a palavra-chave **output** . 

    Por exemplo, a entrada `@model_name` escalar a seguir contém o nome do modelo, que também é apresentado em sua própria coluna nos resultados:

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Todas as variáveis que você passa como parâmetros do procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) devem ser mapeadas para variáveis no código R. Por padrão, as variáveis são mapeadas por nome.

    Todas as colunas no conjunto de dados de entrada também devem ser mapeadas para variáveis no script do R.  Por exemplo, suponha que o script R contenha uma fórmula como esta:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Um erro será gerado se o conjunto de dados de entrada não contiver colunas com os nomes correspondentes ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour e DayOfWeek.

+ Em alguns casos, um esquema de saída deve ser definido com antecedência para os resultados.

    Por exemplo, para inserir os dados em uma tabela, você deve usar a cláusula **with Result Set** para especificar o esquema.

    O esquema de saída também será necessário se o script R usar o `@parallel=1`argumento. O motivo é que vários processos podem ser criados pelo SQL Server para executar a consulta em paralelo, com os resultados coletados no final. Portanto, o esquema de saída deve estar preparado antes que os processos paralelos possam ser criados.
    
    Em outros casos, você pode omitir o esquema de resultado usando a opção **com conjuntos de resultados**indefinidos. Essa instrução retorna o conjunto de dados do script R sem nomear as colunas ou especificar os tipos de dado SQL.

+ Considere a possibilidade de gerar dados de tempo ou de rastreamento usando T-SQL em vez de R.

    Por exemplo, você pode passar a hora do sistema ou outras informações usadas para auditoria e armazenamento adicionando uma chamada T-SQL que é passada para os resultados, em vez de gerar dados semelhantes no script R. 

**Melhorar o desempenho e a segurança**

+ Evite gravar previsões ou resultados intermediários em arquivo. Grave previsões em uma tabela em vez disso, para evitar a movimentação de dados.

+ Execute todas as consultas com antecedência e examine os planos de consulta de SQL Server para identificar as tarefas que podem ser executadas em paralelo.

    Se a consulta de entrada puder ser paralelizada, `@parallel=1` defina como parte de seus argumentos para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    Normalmente, o processamento paralelo com esse sinalizador será possível sempre que o SQL Server puder trabalhar com tabelas particionadas ou distribuir uma consulta entre vários processos e agregar os resultados no final. Normalmente o processamento paralelo com esse sinalizador não será possível se você estiver treinando modelos usando algoritmos que exigem que todos os dados sejam lidos ou se for necessário criar agregações.

+ Examine seu código R para determinar se há etapas que podem ser executadas de maneira independente ou executadas com mais eficiência usando uma chamada de procedimento armazenado separado. Por exemplo, você pode obter melhor desempenho fazendo engenharia de recursos ou extração de recursos separadamente e salvando os valores em uma tabela.

+ Procure maneiras de usar o T-SQL em vez do código R para cálculos com base em conjuntos.

    Por exemplo, esta solução de R mostra como as funções T-SQL definidas pelo usuário e o R podem executar a mesma tarefa de engenharia de recursos: [Instruções de ponta a ponta sobre a ciência de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Se possível, substitua as funções de R  convencionais por funções scaler que dão suporte à execução distribuída. Para obter mais informações, consulte [comparação das funções base r e escala r](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Consulte um desenvolvedor de banco de dados para determinar maneiras de melhorar o desempenho usando SQL Server recursos como [tabelas com otimização de memória](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)ou, se você tiver o Enterprise Edition, [resource governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    Para obter mais informações, consulte [dicas e truques de otimização de SQL Server para o Analytics Services](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>Etapa 3. Preparar para a implantação

+ Notifique o administrador para que os pacotes possam ser instalados e testados antes de implantar seu código. 

    Em um ambiente de desenvolvimento, pode ser bom instalar pacotes como parte do seu código, mas essa é uma prática inadequada em um ambiente de produção. 

    Não há suporte para bibliotecas de usuário, independentemente de você estar usando um procedimento armazenado ou executando o código R no contexto de computação SQL Server.

**Empacotar o código R em um procedimento armazenado**

+ Se o seu código for relativamente simples, você poderá incorporá-lo em uma função definida pelo usuário do T-SQL sem modificação, conforme descrito nestes exemplos:

    + [Criar uma função do R que é executada em rxExec](../tutorials/deepdive-create-a-simple-simulation.md)
    + [Engenharia de recursos usando T-SQL e R](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ Se o código for mais complexo, use o pacote R **sqlrutils** para converter seu código. Este pacote foi criado para ajudar os usuários de R experientes a escreverem um código de procedimento armazenado bom. 

    A primeira etapa é reescrever o código R como uma única função com entradas e saídas claramente definidas.

    Em seguida, use o pacote **sqlrutils** para gerar a entrada e as saídas no formato correto. O pacote **sqlrutils** gera o código de procedimento armazenado completo para você e também pode registrar o procedimento armazenado no banco de dados. 

    Para obter mais informações e exemplos, consulte [sqlrutils (SQL)](ref-r-sqlrutils.md).

**Integre com outros fluxos de trabalho**

+ Aproveite as ferramentas e os processos de ETL do T-SQL. Execute a engenharia de recursos, extração de recursos e limpeza de dados com antecedência como parte dos fluxos de trabalho de dados.

    Quando você está trabalhando em um ambiente [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] de desenvolvimento de R dedicado, como ou RStudio, você pode extrair dados para seu computador, analisar os dados iterativamente e, em seguida, gravar ou exibir os resultados. 
    
    No entanto, quando o código R autônomo é migrado para SQL Server, a maior parte desse processo pode ser simplificada ou delegada a outras ferramentas de SQL Server. 

+ Use estratégias de visualização assíncronas seguras.

    Os usuários do SQL Server geralmente não podem acessar arquivos no servidor, e as ferramentas de cliente do SQL normalmente não dão suporte ao dispositivo de gráficos do R. Se você gerar plotagens ou outros elementos gráficos como parte da solução, considere exportar as plotagens como dados binários e salvar em uma tabela ou escrever.

+ Encapsule funções de previsão e pontuação em procedimentos armazenados para acesso direto por aplicativos.

### <a name="other-resources"></a>Outros recursos

Para exibir exemplos de como uma solução de R pode ser implantada no SQL Server, consulte estes exemplos:

+ [Crie um modelo de previsão para negócios de aluguel de esqui usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Análise no banco de dados para o desenvolvedor do SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) Demonstra como você pode tornar seu código R mais modular encapsulando-o em procedimentos armazenados

+ [Solução de ciência de dados de ponta a ponta](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) Inclui uma comparação da engenharia de recursos em R e T-SQL
