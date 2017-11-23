---
title: "Convertendo código R para uso no R Services | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 06/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d403b716d6be6c571f4de76a25ba3f6f7f5c4e8d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="converting-r-code-for-use-in-r-services"></a>Convertendo o Código de R para Uso no R Services

Quando você move o código R no Studio de R ou outro ambiente para o SQL Server, geralmente o código funciona sem modificações adicionais quando adicionado para o  *@script*  parâmetro [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Isso é especialmente verdadeiro se você tiver desenvolvido em sua solução usando o **RevoScaleR** funções, facilitando relativamente simples para alterar os contextos de execução.

No entanto, normalmente você desejará modificar seu código R para executar no SQL Server, para aproveitar uma integração maior com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e para evitar a cara transferência de dados.

Para exibir exemplos de como o código R pode ser executado no SQL Server, consulte estas instruções passo a passo:

+ [No banco de dados de análise do desenvolvedor do SQL](../tutorials/sqldev-in-database-r-for-sql-developers.md) demonstra como você pode fazer seu código R mais modular encapsulando-os em procedimentos armazenados

+ [Solução de ciência de dados de ponta a ponta](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md) inclui uma comparação de engenharia de recurso em T-SQL e R

## <a name="how-the-data-science-process-changes-in-sql-server"></a>Como o processo de ciência de dados é alterado no SQL Server

Quando você estiver trabalhando em um ambiente de desenvolvimento R dedicado, como [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)] ou RStudio, o fluxo de trabalho típico é para extrair dados em seu computador, analisar os dados interativamente e, em seguida, gravar ou exibir os resultados. No entanto, quando o código de R autônomo é migrado para o SQL Server, grande parte desse processo pode ser simplificado ou delegado para outras ferramentas do SQL Server. Além disso, isso pode melhorar o desempenho em muitos casos.

| Código externo | R no SQL Server |
|-------|-------|
| Ingerir dados| Defina dados de entrada como uma consulta SQL. Evita a movimentação de dados. |
| Resumir e visualizar dados| Gráficos podem ser exportados como imagens ou enviados a uma estação de trabalho remota.|
|Engenharia de recursos| Use o R no banco de dados se você não quiser alterar o seu código, mas examine otimizar suas consultas. Investigue se ele pode ser mais eficiente de chamar funções T-SQL ou UDFs personalizados.|
|Parte de limpeza de dados do processo de análise| Execute engenharia de recurso, a extração do recurso e a limpeza de dados com antecedência como parte dos fluxos de trabalho de dados.|
|Transmitir previsões para o arquivo| Previsões de saída a uma tabela para evitar a movimentação de dados. Wrap prever funções em procedimentos armazenados para acessar diretamente por aplicativos.|

## <a name="best-practices"></a>Práticas recomendadas

+ Tome nota das dependências, como os pacotes necessários, com antecedência. Em um ambiente de teste e de desenvolvimento, pode ser aceitável instalar os pacotes como parte do seu código, mas essa prática não é recomendada em um ambiente de produção. Notifique o administrador para que os pacotes possam ser instalados e testados antes de implantar seu código.

+ Faça uma lista de verificação dos possíveis problemas de tipo de dados. Documente o esquema dos resultados esperados em cada seção do código.

+ Identifique fontes de dados primárias como dados de treinamento de modelo ou dados de entrada para previsões versus fontes secundárias como fatores, variáveis adicionais de agrupamento e assim por diante. Mapeie seu maior conjunto de dados para o parâmetro de entrada de [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Altere suas instruções de dados de entrada para elas trabalharem diretamente no banco de dados. Em vez de mover dados para um arquivo CSV local ou fazendo repetidas chamadas de ODBC, você pode obter um melhor desempenho usando consultas SQL ou exibições que podem ser executadas diretamente no banco de dados, evitando a movimentação de dados.

+ Use planos de consulta do SQL Server para identificar as tarefas que podem ser realizadas em paralelo. Se a consulta de entrada pode ser colocadas em paralelo, defina `@parallel=1` como parte de seus argumentos para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Normalmente, o processamento paralelo com esse sinalizador será possível sempre que o SQL Server puder trabalhar com tabelas particionadas ou distribuir uma consulta entre vários processos e agregar os resultados no final.

  Normalmente o processamento paralelo com esse sinalizador não será possível se você estiver treinando modelos usando algoritmos que exigem que todos os dados sejam lidos ou se for necessário criar agregações.

+ Sempre que possível, substitua as funções R convencionais por funções **ScaleR** que dão suporte à execução distribuída. Para obter mais informações, consulte [funções escala e comparação de Base R](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler-compared-to-base-r).

+ Examine seu código R para determinar se há etapas que podem ser executadas de maneira independente ou executadas com mais eficiência usando uma chamada de procedimento armazenado separado. Por exemplo, você pode decidir realizar a engenharia de recursos ou extração de recursos separadamente e adicionar os valores em uma nova coluna. 

  Use T-SQL em vez do código de R para cálculos com base em conjunto. Para obter um exemplo de uma solução de R que compara UDFs e R para tarefas de engenharia de recurso, consulte [passo a passo de ponta a ponta de ciência de dados](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md).

+ Use o pacote R **sqlrutils** para converter seu código para uma única função com claramente definida de entradas e saídas, que podem ser facilmente mapeadas para parâmetros de procedimento armazenado. Para obter mais informações e exemplos, consulte [SqlRUtils](../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md).


## <a name="restrictions"></a>Restrições

 Tenha em mente as seguintes restrições ao converter seu código R:

### <a name="data-types"></a>Tipos de dados

-   Há suporte para todos os tipos de dados do R. No entanto, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a uma maior variedade de tipos de dados do que o R. Portanto, algumas conversões de tipo de dados implícitos são realizadas ao enviar dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o R e vice-versa. Você talvez precise para explicitamente converter alguns dados.

- Há suporte para valors NULL. R usa o `na` construção de dados para representar um valor ausente, que é semelhante a um valor nulo.

Para obter mais informações, consulte [tipos de dados e bibliotecas de R](../r/r-libraries-and-data-types.md).

### <a name="inputs-and-outputs"></a>Entradas e Saídas

+ É possível definir apenas um conjunto de dados de entrada como parte dos parâmetros de procedimento armazenado. Essa consulta de entrada para o procedimento armazenado pode ser qualquer instrução SELECT única válida. É recomendável que você use essa entrada para o conjunto de dados maior e obter conjuntos de dados menores conforme necessário, usando chamadas para RODBC.

+ Chamadas de procedimento armazenado precedidas por executar não podem ser usadas como uma entrada para [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

+ Todas as colunas no conjunto de dados de entrada devem ser mapeadas para as variáveis no script R. As variáveis são mapeadas automaticamente por nome. Por exemplo, suponha que seu script R contém uma fórmula como esta:
    
    ```R
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek
    ```
    
     Um erro será gerado se o conjunto de dados de entrada não contém colunas com os nomes correspondentes ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour e DayOfWeek.

+ Também é possível fornecer vários parâmetros escalares como entrada. No entanto, quaisquer variáveis que você passar como parâmetros do procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) deverão ser mapeadas para variáveis no código R. Por padrão, as variáveis são mapeadas por nome.

+ Para incluir variáveis escalares de entrada na saída do código R, basta acrescentar a palavra-chave **OUTPUT** ao definir a variável.

+ Em [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], seu código R é limitado à transmissão de um único conjunto de dados como um objeto data.frame. No entanto, também é possível transmitir várias saídas escalares, incluindo gráficos em formato binário e modelos no formato varbinary.

+ Geralmente, é possível transmitir o conjunto de dados retornado pelo script R sem a necessidade de especificar os nomes das colunas de saída, usando a opção WITH RESULT SETS UNDEFINED. Entretanto, quaisquer variáveis no script R que você deseja transmitir devem ser mapeadas para parâmetros de saída do SQL.

+ Se o seu script R usar o argumento `@parallel=1`, será necessário definir o esquema de saída. O motivo é que vários processos podem ser criados pelo SQL Server para executar a consulta em paralelo, com os resultados coletados no final. Portanto, o esquema de saída deve ser definido antes da criação de processos paralelos.

### <a name="dependencies"></a>Dependências

 + Evite instalar pacotes de código R. No SQL Server, os pacotes devem ser instalados com antecedência.
 
  Certifique-se de instalar os pacotes para a biblioteca de pacote padrão usada pelos serviços de aprendizado de máquina. Para obter mais informações, consulte [gerenciamento de pacotes de R para o SQL Server](../r/r-package-management-for-sql-server-r-services.md)
