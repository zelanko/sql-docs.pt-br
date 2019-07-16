---
title: Converter o código R para procedimentos armazenados – serviços do SQL Server Machine Learning
description: Migre o código R para um procedimento armazenado do SQL Server para acesso a dados e de implantação de solução para dados relacionais no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: ac4c00830c9f678c467a75c1531b97fd3723c0b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962719"
---
# <a name="convert-r-code-for-execution-in-sql-server-in-database-instances"></a>Converter o código R para execução em instâncias do SQL Server (no banco de dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece diretrizes de alto nível sobre como modificar o código R para trabalhar no SQL Server. 

Quando você move o código de R do R Studio ou outro ambiente para o SQL Server, com mais frequência o código funcionará sem modificações adicionais: por exemplo, se o código é simples, como uma função que usa algumas entradas e retorna um valor. Ele também é mais fácil para soluções de porta que usam o **RevoScaleR** ou **MicrosoftML** pacotes, que dão suporte à execução em contextos de execução diferentes com alterações mínimas.

No entanto, seu código pode exigir uma alteração significativa se qualquer uma das seguintes opções for aplicável:

+ Você usar bibliotecas de R que acessam a rede ou que não pode ser instalado no SQL Server.
+ O código faz chamadas separadas para fontes de dados fora do SQL Server, como planilhas do Excel, arquivos em compartilhamentos e outros bancos de dados. 
+ Você deseja executar o código a *@script* parâmetro [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e também parametrizar o procedimento armazenado.
+ Sua solução original inclui várias etapas que talvez seja mais eficientes em um ambiente de produção se executada de forma independente, como preparação de dados ou a engenharia de recursos versus modelo de treinamento, pontuação ou relatórios.
+ Você deseja melhorar a otimizar o desempenho, a alteração de bibliotecas, usando execução paralela ou descarregamento de processamento para o SQL Server. 

## <a name="step-1-plan-requirements-and-resources"></a>Etapa 1. Planejar os requisitos e recursos

**Pacotes**

+ Determinar quais pacotes são necessários e certifique-se de que eles funcionam no SQL Server.
 
+ Instale pacotes de antemão, na biblioteca de pacote padrão usada pelos serviços de aprendizado de máquina. Não há suporte para bibliotecas do usuário.

**Fontes de dados** 

+ Se você pretende incorporar código R em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identificar as fontes de dados primários e secundários. 

    + **Primário** fontes de dados são grandes conjuntos de dados, como dados de treinamento do modelo ou dados de entrada para previsões. Planejar mapear seu maior conjunto de dados para o parâmetro de entrada do [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + **Secundário** fontes de dados são normalmente menores conjuntos de dados, como listas de fatores ou variáveis adicionais de agrupamento. 
    
    Atualmente, o sp_execute_external_script dá suporte a apenas um único conjunto de dados como entrada para o procedimento armazenado. No entanto, você pode adicionar várias entradas de escalares ou binárias.

    Chamadas de procedimento armazenado precedidas por EXECUTE não podem ser usadas como uma entrada para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Você pode usar consultas, exibições ou qualquer outra instrução SELECT válida.

+ Determine as saídas que você precisa. Se você executar o código R usando sp_execute_external_script, o procedimento armazenado pode gerar apenas um quadro de dados como resultado. No entanto, também é possível transmitir várias saídas escalares, incluindo gráficos e modelos no formato binário, bem como outros valores escalares derivam do código R ou SQL parâmetros.

**Tipos de dados**

+ Faça uma lista de verificação dos possíveis problemas de tipo de dados.

    Todos os tipos de dados de R têm suporte por serviços de aprendizado de máquina do SQL Server. No entanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a uma maior variedade de tipos de dados que R. Portanto, algumas conversões de tipo de dados implícitos são realizadas ao enviar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados para o R e vice-versa. Talvez seja necessário converter explicitamente ou converter alguns dados. 

    Há suporte para valors NULL. No entanto, o R usa o `na` construção de dados para representar um valor ausente, o que é semelhante a um valor nulo.

+ Considere eliminar a dependência de dados que não podem ser usados pelo r: por exemplo, rowid e tipos de dados GUID do SQL Server não podem ser consumidos por R e gerarem erros.

    Para obter mais informações, consulte [tipos de dados e bibliotecas do R](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Etapa 2. Converter ou reempacotar o código

Quanto você altere seu código depende se você pretende enviar o código de R de um cliente remoto para executar no contexto de computação do SQL Server ou pretende implantar o código como parte de um procedimento armazenado, o que pode fornecer um melhor desempenho e segurança de dados. Quebra automática de seu código em um procedimento armazenado impõe algumas exigências adicionais. 

+ Defina os dados de entrada principais como uma consulta SQL sempre que possível, para evitar a movimentação de dados.

+ Ao executar o R em um procedimento armazenado, você pode passar por meio de vários **escalares** entradas. Para todos os parâmetros que você deseja usar na saída, adicione a **saída** palavra-chave. 

    Por exemplo, a seguinte entrada escalar `@model_name` contém o nome do modelo, que também é a saída em sua própria coluna nos resultados:

    ```sql
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Todas as variáveis que você passar como parâmetros do procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) devem ser mapeados para variáveis no código R. Por padrão, as variáveis são mapeadas por nome.

    Todas as colunas no conjunto de dados de entrada também devem ser mapeadas para variáveis no script R.  Por exemplo, suponha que seu script R contém uma fórmula como esta:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Um erro será gerado se o conjunto de dados de entrada não contém colunas com nomes correspondentes, ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour e DayOfWeek.

+ Em alguns casos, um esquema de saída deve ser definido com antecedência para obter os resultados.

    Por exemplo, para inserir os dados em uma tabela, você deve usar o **com o conjunto de resultados** cláusula para especificar o esquema.

    O esquema de saída também será necessário se o script R usa o argumento `@parallel=1`. O motivo é que vários processos podem ser criados pelo SQL Server para executar a consulta em paralelo, com os resultados coletados no final. Portanto, o esquema de saída deve ser preparado antes da criação de processos paralelos.
    
    Em outros casos, você pode omitir o esquema de resultados usando a opção **WITH RESULT SETS UNDEFINED**. Essa instrução retorna o conjunto de dados do script R, sem nomear as colunas ou especificando os tipos de dados SQL.

+ Considere a geração de dados de rastreamento ou de andamento usando T-SQL em vez de R.

    Por exemplo, você poderia passar a hora do sistema ou outras informações usadas para auditoria e armazenamento pela adição de uma chamada de T-SQL que é passada para os resultados, em vez de gerar dados semelhantes no script R. 

**Melhorar o desempenho e segurança**

+ Evite escrever previsões ou os resultados intermediários em um arquivo. Gravar previsões em uma tabela em vez disso, para evitar a movimentação de dados.

+ Execute todas as consultas com antecedência e examine os planos de consulta do SQL Server para identificar as tarefas que podem ser executadas em paralelo.

    Se a consulta de entrada pode ser paralelizada, defina `@parallel=1` como parte de seus argumentos como [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    Normalmente, o processamento paralelo com esse sinalizador será possível sempre que o SQL Server puder trabalhar com tabelas particionadas ou distribuir uma consulta entre vários processos e agregar os resultados no final. Normalmente o processamento paralelo com esse sinalizador não será possível se você estiver treinando modelos usando algoritmos que exigem que todos os dados sejam lidos ou se for necessário criar agregações.

+ Examine seu código R para determinar se há etapas que podem ser executadas de maneira independente ou executadas com mais eficiência usando uma chamada de procedimento armazenado separado. Por exemplo, você pode obter um melhor desempenho ao fazer a engenharia de recursos ou extração de recursos separadamente e salvar os valores em uma tabela.

+ Buscar formas de usar o T-SQL em vez de código R para cálculos com base em conjunto.

    Por exemplo, esta solução de R mostra funções como definido pelo usuário do T-SQL e R pode realizar a mesma tarefa de engenharia de recurso: [Passo a passo de ponta a ponta de ciência dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Se possível, substitua as funções R convencionais **ScaleR** funções que dão suporte à execução distribuída. Para obter mais informações, consulte [comparação de Base de R e funções de R de escala](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Consulte com um desenvolvedor de banco de dados para determinar maneiras de melhorar o desempenho usando recursos do SQL Server, como [tabelas com otimização de memória](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables), ou, se você tiver a Enterprise Edition [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    Para obter mais informações, consulte [dicas de otimização do SQL Server e truques para os serviços de análise](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>Etapa 3. Preparar para implantação

+ Notifique o administrador para que os pacotes possam ser instalados e testados antes de implantar seu código. 

    Em um ambiente de desenvolvimento, talvez seja okey instalar os pacotes como parte do seu código, mas essa é uma prática ruim em um ambiente de produção. 

    Bibliotecas do usuário não têm suporte, independentemente se você estiver usando um procedimento armazenado ou executando o código de R no contexto de computação do SQL Server.

**Compacte seu código R em um procedimento armazenado**

+ Se seu código é relativamente simple, você pode inseri-la em uma função definida pelo usuário do T-SQL sem modificações, conforme descrito nestes exemplos:

    + [Criar uma função R que é executado em rxExec](../tutorials/deepdive-create-a-simple-simulation.md)
    + [Engenharia de recursos usando o T-SQL e R](../tutorials/sqldev-create-data-features-using-t-sql.md)

+ Se o código é mais complexo, use o pacote R **sqlrutils** para converter seu código. Esse pacote foi projetado para ajudar os usuários experientes do R a escrever código bom procedimento armazenado. 

    A primeira etapa é reescrever o código de R como uma única função com claramente definido de entradas e saídas.

    Em seguida, use o **sqlrutils** pacote para gerar a entrada e saídas no formato correto. O **sqlrutils** pacote gera o código de procedimento armazenado completa para você e também pode registrar o procedimento armazenado no banco de dados. 

    Para obter mais informações e exemplos, consulte [sqlrutils (SQL)](ref-r-sqlrutils.md).

**Integrar com outros fluxos de trabalho**

+ Aproveite as ferramentas de T-SQL e os processos ETL. Execute limpeza de dados com antecedência como parte dos fluxos de trabalho de dados, extração de recursos e engenharia de recursos.

    Quando você estiver trabalhando em um ambiente de desenvolvimento dedicado do R, como [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] ou RStudio, você pode efetuar pull de dados em seu computador, analisá-los interativamente e, em seguida, gravar ou exibir os resultados. 
    
    No entanto, quando o código R autônomo é migrado para o SQL Server, grande parte desse processo pode ser simplificado ou delegado a outras ferramentas do SQL Server. 

+ Use estratégias de visualização segura, assíncrona.

    Os usuários do SQL Server geralmente não é possível acessar arquivos no servidor e ferramentas de cliente SQL normalmente não dão suporte a R graphics device. Se você gerar gráficos ou outros elementos gráficos como parte da solução, considere exportar gráficos como dados binários e salvar em uma tabela ou escrevendo.

+ Encapsule a previsão e as funções de pontuação em procedimentos armazenados para acesso direto por aplicativos.

### <a name="other-resources"></a>Outros recursos

Para exibir exemplos de como uma solução de R pode ser implantada no SQL Server, consulte estes exemplos:

+ [Criar um modelo preditivo para empresas de aluguel de Esqui usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [Análise no banco de dados para o desenvolvedor do SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) demonstra como você pode fazer seu código R mais modular encapsulando-os em procedimentos armazenados

+ [Solução de ciência de dados de ponta a ponta](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) inclui uma comparação de engenharia de recurso em R e T-SQL
