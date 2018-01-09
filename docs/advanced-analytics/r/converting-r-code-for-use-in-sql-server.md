---
title: "Convertendo código R para uso no R Services | Microsoft Docs"
ms.date: 12/20/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 595bdb9cb16b02258d50d1f3d038ad988bbc4dd3
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="converting-r-code-for-execution-in-database"></a>Converter o código de R para execução no banco de dados

Este artigo fornece instruções de alto nível sobre como modificar o código de R para trabalhar no SQL Server. 

Quando você move o código R no Studio de R ou outro ambiente para o SQL Server, geralmente o código funciona sem modificações adicionais: por exemplo, se o código é simples, como uma função que usa algumas entradas e retorna um valor. Também é mais fácil para soluções de porta que usam o **RevoScaleR** ou **MicrosoftML** pacotes, que oferece suporte à execução em contextos de execução diferentes com alterações mínimas.

No entanto, seu código pode exigir alterações substanciais se qualquer uma das seguintes opções for aplicável:

+ Você usar bibliotecas de R que acessam a rede ou que não pode ser instalado no SQL Server.
+ O código faz chamadas separadas para fontes de dados fora do SQL Server, como planilhas do Excel, arquivos em compartilhamentos e outros bancos de dados. 
+ Você deseja executar o código de  *@script*  parâmetro [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e também parametrizar o procedimento armazenado.
+ Sua solução original inclui várias etapas que podem ser mais eficientes em um ambiente de produção se executadas independentemente, como preparação de dados ou de engenharia de recurso versus modelo de treinamento, classificação ou relatório.
+ Você deseja melhorar a otimizar o desempenho alterando bibliotecas, usando a execução paralela ou descarregamento de algum processamento para o SQL Server. 

## <a name="step-1-plan-requirements-and-resources"></a>Etapa 1. Planejar os requisitos e recursos

**Pacotes**

+ Determinar quais pacotes são necessários e certifique-se de que eles funcionam no SQL Server.
 
+ Instale pacotes com antecedência, a biblioteca de pacote padrão usada pelos serviços de aprendizado de máquina. Não há suporte para bibliotecas do usuário.

**Fontes de Dados** 

+ Se você pretende inserir o código de R [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), identificar as fontes de dados primários e secundários. 

    + **Primário** fontes de dados são grandes conjuntos de dados, como dados de treinamento do modelo ou dados de entrada para previsões. Planejar mapear o maior conjunto de dados para o parâmetro de entrada de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

    + **Secundário** fontes de dados são geralmente menores conjuntos de dados, como listas de fatores ou variáveis de agrupamento adicional. 
    
    Atualmente, o sp_execute_external_script oferece suporte a apenas um único conjunto de dados como entrada para o procedimento armazenado. No entanto, você pode adicionar várias entradas de escalares ou binárias.

    Chamadas de procedimento armazenado precedidas por executar não podem ser usadas como uma entrada para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Você pode usar consultas, exibições ou qualquer outra instrução SELECT válida.

+ Determine as saídas que você precisa. Se você executar código R usando sp_execute_external_script, o procedimento armazenado pode produzir um quadro de dados como resultado. No entanto, você também pode gerar várias saídas escalares, incluindo gráficos e modelos no formato binário, bem como outros valores escalares derivam do SQL ou código R parâmetros.

**Tipos de dados**

+ Faça uma lista de verificação dos possíveis problemas de tipo de dados.

    Todos os tipos de dados R têm suporte pelos serviços de aprendizado de máquina do SQL Server. No entanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a uma maior variedade de tipos de dados que R. Portanto, algumas conversões de tipo de dados implícitas são executadas durante o envio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados em R e vice-versa. Talvez seja necessário converter explicitamente ou converter alguns dados. 

    Há suporte para valors NULL. No entanto, R usa o `na` construção de dados para representar um valor ausente, que é semelhante a um valor nulo.

+ Considere eliminar a dependência de dados não podem ser usados por r: por exemplo, rowid e tipos de dados GUID do SQL Server não podem ser consumidos por R e gerarem erros.

    Para obter mais informações, consulte [tipos de dados e bibliotecas de R](../r/r-libraries-and-data-types.md).

## <a name="step-2-convert-or-repackage-code"></a>Etapa 2. Converter ou remontar o código

Quanto você alterar o código depende se você pretende enviar o código de R de um cliente remoto para ser executado no contexto de computação do SQL Server, ou pretende implantar o código como parte de um procedimento armazenado, o que pode oferecer melhor desempenho e segurança de dados. Encapsular seu código em um procedimento armazenado impõe algumas exigências adicionais. 

+ Defina os dados de entrada principais como uma consulta SQL sempre que possível, para evitar a movimentação de dados.

+ Ao executar R em um procedimento armazenado, você pode passar por meio de vários **escalar** entradas. Para todos os parâmetros que você deseja usar na saída, adicione o **saída** palavra-chave. 

    Por exemplo, a seguinte entrada escalar `@model_name` contém o nome do modelo, que também é a saída em sua própria coluna nos resultados:

    ```SQL
    EXEC sp_execute_external_script @model_name="DefaultModel" OUTPUT, @language=N'R', @script=N'R code here'
    ``` 

+ Todas as variáveis que você passar como parâmetros do procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) devem ser mapeados para variáveis no código R. Por padrão, as variáveis são mapeadas por nome.

    Todas as colunas do conjunto de dados de entrada também devem ser mapeadas para variáveis no script R.  Por exemplo, suponha que seu script R contém uma fórmula como esta:

    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
    Um erro será gerado se o conjunto de dados de entrada não contém colunas com os nomes correspondentes ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour e DayOfWeek.

+ Em alguns casos, um esquema de saída deve ser definido com antecedência para os resultados.

    Por exemplo, para inserir os dados em uma tabela, você deve usar o **com o conjunto de resultados** cláusula para especificar o esquema.

    O esquema de saída também é necessário se o script de R usa o argumento `@parallel=1`. O motivo é que vários processos podem ser criados pelo SQL Server para executar a consulta em paralelo, com os resultados coletados no final. Portanto, o esquema de saída deve ser preparado antes da criação de processos paralelos.
    
    Em outros casos, você pode omitir o esquema de resultados usando a opção **com RESULT SETS UNDEFINED**. Esta instrução retorna o conjunto de dados do script R sem nomear as colunas ou especificando os tipos de dados SQL.

+ Considere gerar dados de rastreamento ou de andamento usando o T-SQL em vez de R.

    Por exemplo, você poderia passar a hora do sistema ou outras informações utilizadas para armazenamento de auditoria e adição de uma chamada de T-SQL que é passada para os resultados, em vez de gerar dados semelhantes no script R. 

**Melhorar o desempenho e segurança**

+ Evite escrever previsões ou resultados intermediários no arquivo. Grave previsões em uma tabela em vez disso, para evitar a movimentação de dados.

+ Execute todas as consultas com antecedência e examine os planos de consulta do SQL Server para identificar as tarefas que podem ser executadas em paralelo.

    Se a consulta de entrada pode ser colocadas em paralelo, defina `@parallel=1` como parte de seus argumentos para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). 

    Normalmente, o processamento paralelo com esse sinalizador será possível sempre que o SQL Server puder trabalhar com tabelas particionadas ou distribuir uma consulta entre vários processos e agregar os resultados no final. Normalmente o processamento paralelo com esse sinalizador não será possível se você estiver treinando modelos usando algoritmos que exigem que todos os dados sejam lidos ou se for necessário criar agregações.

+ Examine seu código R para determinar se há etapas que podem ser executadas de maneira independente ou executadas com mais eficiência usando uma chamada de procedimento armazenado separado. Por exemplo, você pode obter um melhor desempenho fazendo engenharia de recurso ou extração de um recurso separadamente e salvar os valores em uma tabela.

+ Procure maneiras de usar o T-SQL em vez do código de R para cálculos com base em conjunto.

    Por exemplo, esta solução R mostra como-funções definidas pelo usuário T-SQL e R pode executar a mesma tarefa de engenharia de recurso: [passo a passo de ponta a ponta de ciência de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Se possível, substitua convencionais funções de R com **ScaleR** funções que oferece suporte à execução distribuída. Para obter mais informações, consulte [funções escala e comparação de Base R](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Consultar um desenvolvedor de banco de dados para determinar maneiras de melhorar o desempenho usando os recursos do SQL Server, como [tabelas com otimização de memória](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables), ou, se você tiver a Enterprise Edition, [Resource Governor](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)).

    Para obter mais informações, consulte [dicas de otimização do SQL Server e truques para serviços de análise](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

### <a name="step-3-prepare-for-deployment"></a>Etapa 3. Preparar para implantação

+ Notifique o administrador para que os pacotes possam ser instalados e testados antes de implantar seu código. 

    Em um ambiente de desenvolvimento, ele pode ser okey instalar os pacotes como parte do seu código, mas essa é uma prática incorreta em um ambiente de produção. 

    Bibliotecas de usuário não têm suporte, independentemente se você estiver usando um procedimento armazenado ou executando o código R no contexto de computação do SQL Server.

**Empacotar seu código R em um procedimento armazenado**

+ Se seu código é relativamente simple, você pode inseri-lo em uma função definida pelo usuário do T-SQL sem modificação, conforme descrito nesses exemplos:

    + [Criar uma função de R que é executado em rxExec](..\tutorials\deepdive-create-a-simple-simulation.md)
    + [Engenharia de recurso usando o T-SQL e R](..\tutorials\sqldev-create-data-features-using-t-sql.md)

+ Se o código for mais complexo, use o pacote R **sqlrutils** para converter seu código. Esse pacote foi projetado para ajudar usuários experientes do R a escrever código bom procedimento armazenado. 

    A primeira etapa é reescrever o código de R como uma única função com claramente definidas entradas e saídas.

    Em seguida, use o **sqlrutils** pacote para gerar a entrada e saída no formato correto. O **sqlrutils** pacote gera o código de procedimento armazenado completa para você e também pode registrar o procedimento armazenado no banco de dados. 

    Para obter mais informações e exemplos, consulte [SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md).

**Integrar com outros fluxos de trabalho**

+ Utilizar ferramentas de T-SQL e os processos ETL. Execute engenharia de recurso, a extração do recurso e a limpeza de dados com antecedência como parte dos fluxos de trabalho de dados.

    Quando você estiver trabalhando em um ambiente de desenvolvimento R dedicado, como [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] ou RStudio, você pode extrair dados em seu computador, analisar os dados interativamente e, em seguida, gravar ou exibir os resultados. 
    
    No entanto, quando o código de R autônomo é migrado para o SQL Server, grande parte desse processo pode ser simplificado ou delegado para outras ferramentas do SQL Server. 

+ Use as estratégias de visualização segura e assíncrona.

    Os usuários do SQL Server geralmente não podem acessar arquivos no servidor e ferramentas de cliente SQL normalmente não oferecem suporte a dispositivo de gráficos de R. Se você gerar gráficos ou outros elementos gráficos como parte da solução, considere exportar os gráficos como dados binários e salvando em uma tabela ou gravação.

+ Encapsule previsão e as funções de pontuação em procedimentos armazenados para acessar diretamente por aplicativos.

### <a name="other-resources"></a>Outros recursos

Para exibir exemplos de como uma solução R pode ser implantada no SQL Server, consulte estes exemplos:

+ [Criar um modelo de previsão para empresas de aluguel ski usando R e SQL Server](https://microsoft.github.io/sql-ml-tutorials/R/rentalprediction/)

+ [No banco de dados de análise do desenvolvedor do SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) demonstra como você pode fazer seu código R mais modular encapsulando-os em procedimentos armazenados

+ [Solução de ciência de dados de ponta a ponta](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) inclui uma comparação de engenharia de recurso em T-SQL e R
