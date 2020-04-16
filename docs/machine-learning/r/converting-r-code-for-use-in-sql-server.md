---
title: Converter o código R para SQL
description: Migre o código R para um procedimento armazenado do SQL Server para implantação de soluções e acesso a dados relacionais no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 97bb0a54181f88703363bfbe598af26ede58ebf8
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117709"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>Converter código R para execução em instâncias do SQL Server (no banco de dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo fornece diretrizes de alto nível sobre como modificar o código R para trabalhar no SQL Server. 

Quando você move o código R do R Studio ou de outro ambiente para o SQL Server, geralmente o código funciona sem modificações adicionais. Isso ocorre, por exemplo, quando o código é simples, assim como uma função que usa algumas entradas e retorna um valor. Também é mais fácil migrar soluções que usam o **RevoScaleR** ou pacotes do **MicrosoftML**, que oferecem suporte à execução em contextos de execução diferentes com alterações mínimas.

No entanto, seu código poderá exigir alterações substanciais em qualquer um dos seguintes casos:

+ Você usa bibliotecas do R que acessam a rede ou que não podem ser instaladas no SQL Server.
+ O código faz chamadas separadas para fontes de dados fora do SQL Server, tais como planilhas do Excel, arquivos em compartilhamentos e outros bancos de dados. 
+ Você deseja executar o código no parâmetro *\@script* de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e também parametrizar o procedimento armazenado.
+ Sua solução original inclui várias etapas que, caso executadas de modo independente, podem ser mais eficientes em um ambiente de produção, assim como preparação de dados ou engenharia de recursos versus treinamento de modelo, pontuação ou relatório.
+ Você deseja otimizar o desempenho alterando as bibliotecas, usando a execução paralela ou descarregando algum processamento para o SQL Server. 

## <a name="step-1-plan-requirements-and-resources"></a>Etapa 1. Recursos e requisitos do plano

**Pacotes**

+ Determine quais pacotes são necessários e verifique se eles funcionam no SQL Server.
 
+ Instale pacotes com antecedência, na biblioteca de pacotes padrão usada pelos Serviços de Machine Learning. Bibliotecas de usuário não são compatíveis.

**Fontes de dados** 

+ Se pretender inserir o código R em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identifique as fontes de dados primárias e secundárias. 

    + As fontes de dados **primárias** são grandes conjuntos de dados, tais como os de treinamento de modelo ou dados de entrada para previsões. Planeje o mapeamento do seu maior conjunto de dados para o parâmetro de entrada [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + As fontes de dados **secundárias** normalmente são conjuntos de dados menores, tais como listas de fatores ou variáveis de agrupamento adicionais. 
    
    Atualmente, sp_execute_external_script dá suporte a apenas um único conjunto de dados como entrada para o procedimento armazenado. No entanto, você pode adicionar várias entradas escalares ou binárias.

    As chamadas de procedimento armazenado precedidas por EXECUTE não podem ser usadas como uma entrada para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Você pode usar consultas, exibições ou qualquer outra instrução SELECT válida.

+ Determine as saídas que você precisa. Se você executar o código R usando sp_execute_external_script, o procedimento armazenado poderá gerar como resultado apenas uma estrutura de dados. No entanto, você também pode gerar várias saídas escalares, incluindo plotagens e modelos em formato binário, bem como outros valores escalares derivados de código R ou parâmetros SQL.

**Tipos de dados**

+ Faça uma lista de verificação dos possíveis problemas de tipo de dados.

    Todos os tipos de dados do R são compatíveis com os Serviços de Machine Learning do SQL Server. No entanto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a uma maior variedade de tipos de dados do que o R. Portanto, algumas conversões de tipo de dados implícitos são realizadas ao enviar dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o R e vice-versa. Talvez seja necessário converter explicitamente alguns dados. 

    Há suporte para valors NULL. No entanto, o R usa o constructo de dados `na` para representar um valor ausente, semelhante um nulo.

+ Considere eliminar as dependências de dados que não podem ser usadas pelo R: por exemplo, os tipos de dados rowid e GUID do SQL Server não podem ser consumidos pelo R, portanto, tampouco podem gerar erros.

    Para obter mais informações, confira [Tipos de dados e bibliotecas do R](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Etapa 2. Converter ou reempacotar código

O quanto você altera o seu código depende de você pretender enviar o código R de um cliente remoto para ser executado no contexto de computação do SQL Server ou pretender implantar o código como parte de um procedimento armazenado, o que pode oferecer segurança de dados e desempenho melhores. Encapsular seu código em um procedimento armazenado impõe alguns requisitos adicionais. 

+ Defina os dados de entrada primários como uma consulta SQL sempre que possível, para evitar movimentação de dados.

+ Ao executar o R em um procedimento armazenado, você pode passar várias entradas **escalares**. Para todos os parâmetros que você deseja usar na saída, adicione a palavra-chave **OUTPUT**. 

    Por exemplo, o `@model_name` de entrada escalar a seguir contém o nome do modelo, que também é apresentado em sua própria coluna nos resultados:

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Quaisquer variáveis que você passar como parâmetros do procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) deverão ser mapeadas para variáveis no código R. Por padrão, as variáveis são mapeadas por nome.

    Todas as colunas no conjunto de dados de entrada também devem ser mapeadas para as variáveis no script R.  Por exemplo, digamos que seu script R contenha uma fórmula como esta:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Será gerado um erro se o conjunto de dados de entrada não contiver colunas com nomes correspondentes, ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour e DayOfWeek.

+ Em alguns casos, um esquema de saída deverá ser definido com antecedência para os resultados.

    Por exemplo, para inserir os dados em uma tabela, você deve usar a cláusula **WITH RESULT SET** para especificar o esquema.

    O esquema de saída também será necessário se o script R usar o argumento `@parallel=1`. O motivo é que vários processos podem ser criados pelo SQL Server para executar a consulta em paralelo, com os resultados coletados no final. Portanto, o esquema de saída precisa ser preparado, para que então seja possível criar processos paralelos.
    
    Em outros casos, você pode omitir o esquema de resultados usando a opção **WITH RESULT SETS UNDEFINED**. Essa instrução retorna o conjunto de dados do script R sem nomear as colunas nem especificar os tipos de dados do SQL.

+ Considere a possibilidade de gerar dados de tempo ou de acompanhamento usando T-SQL em vez de R.

    Por exemplo, você pode passar a hora do sistema ou outras informações usadas para auditoria e armazenamento adicionando uma chamada T-SQL que é passada para os resultados, em vez de gerar dados semelhantes no script R. 

**Melhorar o desempenho e a segurança**

+ Evite gravar previsões ou resultados intermediários em arquivo. Em vez disso, grave previsões em uma tabela, a fim de evitar a movimentação de dados.

+ Execute todas as consultas antecipadamente e examine os planos de consulta do SQL Server para identificar as tarefas que podem ser realizadas em paralelo.

    Se a consulta de entrada puder ser paralelizada, defina `@parallel=1` como parte de seus argumentos como [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    Normalmente, o processamento paralelo com esse sinalizador será possível sempre que o SQL Server puder trabalhar com tabelas particionadas ou distribuir uma consulta entre vários processos e agregar os resultados no final. Normalmente o processamento paralelo com esse sinalizador não será possível se você estiver treinando modelos usando algoritmos que exigem que todos os dados sejam lidos ou se for necessário criar agregações.

+ Examine seu código R para determinar se há etapas que podem ser executadas de maneira independente ou executadas com mais eficiência usando uma chamada de procedimento armazenado separado. Por exemplo, você pode obter um melhor desempenho realizando a engenharia de recursos ou a extração de recursos separadamente e salvando os valores em uma tabela.

+ Procure meios de usar T-SQL em vez de código R para computação baseada em conjunto.

    Por exemplo, esta solução de R mostra como as funções T-SQL definidas pelo usuário e o R podem executar a mesma tarefa de engenharia de recursos: [Passo a passo de ponta a ponta sobre a ciência de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Se possível, substitua as funções R convencionais por funções **ScaleR** que dão suporte à execução distribuída. Para obter mais informações, confira [Comparação de funções em Base R e Scale R](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Consulte um desenvolvedor de banco de dados para determinar maneiras de melhorar o desempenho usando recursos do SQL Server como as [tabelas com otimização de memória](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables) ou, se você tiver a Edição Enterprise, o [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor).

    Para obter mais informações, confira [Dicas e truques de otimização do SQL Server para serviços analíticos](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>Etapa 3. Preparar para a implantação

+ Notifique o administrador para que os pacotes possam ser instalados e testados antes de implantar seu código. 

    Em um ambiente de desenvolvimento, pode ser aceitável instalar os pacotes como parte do seu código, mas essa prática não é recomendada em um ambiente de produção. 

    O uso de bibliotecas de usuário não é compatível, independentemente de você estar usando um procedimento armazenado ou executando o código R no contexto de computação do SQL Server.

**Empacotar o código R em um procedimento armazenado**

+ Se o código for relativamente simples, você poderá inseri-lo sem modificações a uma função do T-SQL definida pelo usuário, conforme descrito nestes exemplos:

    + [Engenharia de recursos usando T-SQL e R](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ Se o código for mais complexo, use o pacote do R **sqlrutils** para converter seu código. Este pacote foi criado para ajudar os usuários de R experientes a escreverem um código de procedimento armazenado de boa qualidade. 

    A primeira etapa é reescrever o código R como uma única função, com entradas e saídas claramente definidas.

    Em seguida, use o pacote **sqlrutils** para gerar a entrada e as saídas no formato correto. O pacote **sqlrutils** gera o código de procedimento armazenado completo para você. Você também pode registrar o procedimento armazenado no banco de dados. 

    Para obter mais informações e exemplos, confira [sqlrutils (SQL)](ref-r-sqlrutils.md).

**Integrar com outros fluxos de trabalho**

+ Aproveite as ferramentas de T-SQL e os processos de ETL. Realize engenharia de recursos, extração de recursos e limpeza de dados com antecedência como parte dos fluxos de trabalho de dados.

    Quando você estiver trabalhando em um ambiente de desenvolvimento R dedicado, tal como o [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] ou o RStudio, você poderá efetuar pull dos dados para seu computador, analisá-los interativamente e então registrar ou exibir os resultados. 
    
    No entanto, quando o código R autônomo é migrado para o SQL Server, grande parte desse processo pode ser simplificado ou delegado a outras ferramentas do SQL Server. 

+ Use estratégias de visualização assíncronas e seguras.

    Os usuários do SQL Server geralmente não podem acessar arquivos no servidor e as ferramentas de cliente do SQL normalmente não dão suporte ao dispositivo de gráficos do R. Se você gerar plotagens ou outros elementos gráficos como parte da solução, considere exportar os gráficos como dados binários e salvá-los em uma tabela ou registrá-los.

+ Encapsule funções de previsão e pontuação em procedimentos armazenados para que aplicativos tenham acesso direto a elas.

### <a name="other-resources"></a>Outros recursos

Para exibir exemplos de como uma solução de R pode ser implantada no SQL Server, confira estes exemplos:

+ [Criar um modelo preditivo para negócios de aluguel de esqui usando o R e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Análise interna no banco de dados para o desenvolvedor de SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) Demonstra como é possível tornar seu código R mais modular encapsulando-o em procedimentos armazenados

+ [Solução de ciência de dados de ponta a ponta](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) Inclui uma comparação de engenharia de recursos em R e no T-SQL
