---
title: "Convertendo c&#243;digo R para uso em servi&#231;os de R | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Convertendo c&#243;digo R para uso em servi&#231;os de R
Quando você move o código R do Studio de R ou outro ambiente para o SQL Server, muitas vezes o código funcionará sem alteração adicional quando adicionado para o *@script* parâmetro do [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Isso é especialmente verdadeiro se você desenvolveu sua solução usando as funções ScaleR, tornando relativamente simples para alterar os contextos de execução.    
    
No entanto, normalmente você desejará modificar seu código R para executar no SQL Server, para tirar proveito de uma integração maior com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e para evitar a cara transferência de dados.   
   
   
## Recursos  
  
Para exibir exemplos de como executar código R no SQL Server, consulte essa instruções passo a passo:   
+ [No banco de dados análise para o desenvolvedor SQL](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)    
  Demonstra como você pode tornar seu código R mais modular, encapsulá-la em procedimentos armazenados  
+ [Solução de ciência de dados de ponta a ponta](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)    
  Inclui uma comparação de engenharia de recurso em R e T-SQL

## Alterações no processo de ciência de dados no SQL Server  
  
Quando você estiver trabalhando em [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)], RStudio, ou outro ambiente, um fluxo de trabalho típico é extrair os dados em seu computador, analisar os dados interativamente e escrever ou exibir os resultados. No entanto, quando o código autônomo R é migrado para o SQL Server, grande parte desse processo pode ser simplificado ou delegada a outras ferramentas do SQL Server:

| Código externo | R no SQL Server |
|-------|-------|
| Ingestão de dados| Definir dados de entrada como uma consulta SQL no banco de dados | 
| Resumir e visualizar dados| Nenhuma alteração; gráficos podem ser exportados como imagens ou enviados para uma estação de trabalho remota|
|Engenharia de recursos| Você pode usar o R no banco de dados, mas pode ser mais eficiente de chamar funções T-SQL ou UDFs personalizados|
|Parte do processo de análise de limpeza de dados| Limpeza de dados pode ser delegada aos processos de ETL e executada com antecedência|
|Previsões de saída em um arquivo| Previsões para encapsular ou da tabela de saída `predict` em procedimentos armazenados para acesso direto por aplicativos|
  

  
## Práticas recomendadas  
  
+ Tome nota das dependências, como os pacotes necessários com antecedência. Em um ambiente de teste e desenvolvimento, talvez seja bom instalar os pacotes como parte do seu código, mas essa é uma prática ruim em um ambiente de produção. Notificar o administrador para que os pacotes podem ser instalados e testados antes de implantar seu código.  
+ Faça uma lista de verificação de dados possíveis problemas de tipo. Documente os esquemas dos resultados esperados em cada seção do código.  
+ Identificar as fontes de dados principais, como dados de treinamento do modelo ou dados de entrada para previsões versus fontes secundárias como fatores, variáveis adicionais de agrupamento e assim por diante. Mapear o maior conjunto de dados para o parâmetro de entrada do [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).  
+ Altere suas instruções de dados de entrada para trabalhar diretamente no banco de dados. Em vez de mover dados para um arquivo CSV local ou fazendo repetidas chamadas de ODBC, você obterá melhor desempenho usando consultas SQL ou exibições que podem ser executadas diretamente no banco de dados, evitando a movimentação de dados.  
+ Use a planos de consulta do SQL Server para identificar as tarefas que podem ser executadas em paralelo. Se a consulta de entrada pode ser colocado em paralelo, defina `@parallel=1` como parte de seus argumentos para sp_execute_external_script. Processamento com esse sinalizador paralelo é normalmente possível sempre que a do SQL Server pode trabalhar com tabelas particionadas ou distribuir uma consulta entre vários processos e agregar os resultados no final. 
   Processamento com esse sinalizador paralelo normalmente não é possível se você estiver usando algoritmos que exigem todos os dados a serem lidos de modelos de treinamento, ou se você precisar criar agregações. 
+ Sempre que possível, substitua convencionais funções R com **ScaleR** funções que oferece suporte à execução distribuída. Para obter mais informações, consulte [comparação de funções em escala R e R CRAN](Summary%20of%20rx%20Functions.md).
+ Revise seu código R para determinar se há etapas que podem ser executadas de maneira independente ou executadas com mais eficiência usando uma chamada de procedimento armazenado separado. Por exemplo, você pode decidir realizar a extração de engenharia ou recurso do recurso separadamente e adicione os valores em uma nova coluna. Use T-SQL em vez de código R para computação baseada em conjunto. Para obter um exemplo de uma solução de R que compara o desempenho das UDFs e R para tarefas de engenharia de recurso, consulte este tutorial: [passo a passo de ponta a ponta de ciência de dados](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md).  
  
    
## Restrições    
 Tenha em mente as seguintes restrições ao converter seu código R:    
   
**Tipos de dados**    
-   Há suporte para todos os tipos de dados de R. No entanto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a uma grande variedade de tipos de dados que R, portanto algumas conversões de tipo de dados implícitas são executadas ao enviar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados r e vice-versa. Você também precisará explicitamente cast ou converter alguns dados.    
    
- Há suporte para valores nulos. R usa a `na` dados construir para representar valores ausentes, que é semelhante em relação a nulls.    
    
- Para obter mais informações, consulte [Trabalhando com tipos de dados R](../../advanced-analytics/r-services/working-with-r-data-types.md).    
 
 **Entradas e saídas**   
+ Você pode definir apenas um conjunto de dados de entrada como parte dos parâmetros de procedimento armazenado. Essa consulta de entrada para o procedimento armazenado pode ser qualquer instrução SELECT única válida. É recomendável que você use essa entrada para o conjunto de dados maior e obter conjuntos de dados menores, se necessário, usando chamadas para RODBC. 

+ Chamadas precedidas EXECUTE não podem ser usadas como entrada para sp_execute_external_script do procedimento armazenado.    
    
+ Todas as colunas no conjunto de dados devem ser mapeadas para as variáveis no script R. As variáveis são mapeadas automaticamente por nome. Por exemplo, digamos que seu script R contém uma fórmula como esta:    
    
    ```    
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek    
    ```    
    
     Um erro será gerado se o conjunto de dados de entrada não contém colunas com nomes correspondentes, ArrDelay, CRSDepTime, DayOfWeek, CRSDepHour e DayOfWeek.    

+ Você também pode fornecer vários parâmetros escalares como entrada. No entanto, todas as variáveis que você passa como parâmetros do procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) devem ser mapeados para variáveis no código R. Por padrão, as variáveis são mapeadas por nome.
+ Para incluir variáveis escalares de entrada na saída do código R, basta acrescentar o **saída** palavra-chave quando você define a variável.             
+ Em [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], seu código R é limitado à saída de um único conjunto de dados como um objeto Frame. No entanto, você também pode gerar escalar várias saídas, incluindo gráficos em formato binário e modelos no formato varbinary.    
    
+ Geralmente, você pode produzir o conjunto de dados retornado pelo script R sem a necessidade de especificar os nomes das colunas de saída, usando a opção com RESULT SETS UNDEFINED. Entretanto, todas as variáveis no script R que você deseja dar saída devem ser mapeadas para parâmetros de saída do SQL.
    
+ Se o seu script R usa o argumento `@parallel=1`, você deve definir o esquema de saída. O motivo é que vários processos possam ser criados pelo SQL Server para executar a consulta em paralelo, com os resultados coletados no final. Portanto, o esquema de saída deve ser definido antes da criação de processos paralelos.

 **Dependências**
 + Evite a instalação de pacotes de código R. No SQL Server, os pacotes devem ser instalados com antecedência.  
  
  
  

