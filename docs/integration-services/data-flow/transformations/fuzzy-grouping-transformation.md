---
title: "Transforma&#231;&#227;o Agrupamento Difuso | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.fuzzygroupingtrans.f1"
helpviewer_keywords: 
  - "limpando dados"
  - "comparando dados"
  - "delimitadores de token [Integration Services]"
  - "índices temporários [Integration Services]"
  - "transformação Agrupamento Difuso"
  - "tabelas temporárias [Integration Services]"
  - "agrupando dados"
  - "padronizando dados [Integration Services]"
  - "colunas [Integration Services], padronizando"
  - "limites de similaridade [Integration Services]"
  - "limpeza de dados [Integration Services]"
  - "dados duplicados [Integration Services]"
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
caps.latest.revision: 58
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# Transforma&#231;&#227;o Agrupamento Difuso
  A transformação Agrupamento Difuso executa tarefas de limpeza de dados identificando linhas de dados que provavelmente sejam duplicatas e selecionando uma linha canônica de dados a ser usada na padronização dos dados.  
  
> [!NOTE]  
>  Para obter informações mais detalhadas sobre transformação de Agrupamento Difuso, incluindo limitações de desempenho e de memória, consulte o white paper, [Pesquisa Difusa e Agrupamento Difuso no SQL Server Integration Services 2005](http://go.microsoft.com/fwlink/?LinkId=96604).  
  
 A transformação Agrupamento Difuso requer uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para criar tabelas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] temporárias que o algoritmo de transformação necessita para executar seu trabalho. A conexão deve determinar um usuário que tenha permissão para criar tabelas no banco de dados.  
  
 Para configurar a transformação, você deve selecionar as colunas de entrada a serem usadas para identificar duplicatas e selecionar o tipo de correspondência – difusa ou exata – para cada coluna. A correspondência exata garante que somente as linhas com valores idênticos na coluna sejam agrupadas. A correspondência exata pode ser se aplicada a colunas de qualquer tipo de dados do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], exceto DT_TEXT, DT_NTEXT e DT_IMAGE. Uma correspondência difusa agrupa linhas que têm aproximadamente os mesmos valores. O método para correspondência aproximada de dados é baseado em uma pontuação de similaridade especificada pelo usuário. Só colunas com os  tipos de dados DT_WSTR e DT_STR podem ser usadas em correspondência difusa. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 A saída de transformação inclui todas as colunas de entrada, uma ou mais colunas com dados padronizados, e uma coluna que contém a pontuação de similaridade. A pontuação é um valor decimal entre 0 e 1. A linha canônica tem a pontuação 1. Outras linhas do grupo difuso têm pontuações que indicam a qualidade da correspondência entre a linha e a linha canônica. Quanto mais próxima de 1 for a pontuação, mais próxima será a correspondência da fila com a fila canônica. Se o grupo difuso tiver linhas duplicatas exatas da linha canônica, essas linhas também receberão pontuação 1. A transformação não remove linhas duplicadas; ela as agrupa, criando uma chave que associa a linha canônica a linhas similares.  
  
 A transformação produz uma linha de saída para cada linha de entrada, com as seguintes colunas adicionais:  
  
-   **_key_in**, uma coluna que identifica exclusivamente cada linha.  
  
-   **_key_out**, uma coluna que identifica um grupo de linhas duplicadas. A coluna **_key_out** tem o valor da coluna **_key_in** na linha de dados canônica. Linhas com o mesmo valor em **_key_out** fazem parte do mesmo grupo. O valor **_key_out** de um grupo corresponde ao valor **_key_in** na linha de dados canônica.  
  
-   **_score**, um valor entre 0 e 1 que indica a semelhança da linha de entrada à linha canônica.  
  
 Esses são os nomes de coluna padrão e você pode configurar a transformação Agrupamento Difuso para usar outros nomes. A saída também fornece uma pontuação de similaridade para cada coluna que participa de um agrupamento difuso.  
  
 A transformação Agrupamento Difuso inclui dois recursos para personalizar o agrupamento que ela executa: delimitadores de token e limite de similaridade. A transformação fornece um conjunto padrão de delimitadores para criar tokens de dados, mas você pode adicionar novos delimitadores que melhoram essa criação.  
  
 O limite de similaridade indica como a transformação identifica rigidamente duplicatas. Os limites de similaridade podem ser definidos nos níveis de componente e de coluna. O limite de similaridade no nível de coluna só está disponível para as colunas que realizam a correspondência difusa. O intervalo de similaridade é de 0 a 1. Quanto mais próximo de 1 for o limite, mais similares as linhas e colunas devem ser para se qualificarem como duplicatas. Você especifica o limite de similaridade entre linhas e colunas definindo a propriedade MinSimilarity nos níveis de componente e coluna. Para satisfazer a similaridade que é especificada no nível de componente, todas as linhas devem ter uma similaridade por todas as colunas que seja maior ou igual ao limite de similaridade especificado no nível de componente.  
  
 A transformação Agrupamento Difuso calcula medidas internas de similaridade, e as linhas que são menos similares do que o valor especificado em MinSimilarity não são agrupados.  
  
 Para identificar um limite de similaridade que funcione para os seus dados, talvez seja preciso aplicar a transformação Agrupamento Difuso várias vezes usando limites de similaridade mínimos diferentes. No tempo de execução, as colunas de pontuação na saída de transformação contêm as pontuações de similaridade para cada linha do grupo. Você pode usar esses valores para identificar o limite de similaridade adequado para os seus dados. Se você quiser aumentar a similaridade, defina MinSimilarity como um valor maior que o valor nas colunas de pontuação.  
  
 Você pode personalizar o agrupamento que a transformação executa definindo as propriedades das colunas na entrada de transformação Agrupamento Difuso. Por exemplo, a propriedade FuzzyComparisonFlags especifica como a transformação compara os dados de cadeia de caracteres em uma coluna, e a propriedade ExactFuzzy especifica se a transformação executa uma correspondência difusa ou exata.  
  
 A quantidade de memória que a transformação Agrupamento Difuso usa pode ser configurada definindo a propriedade personalizada MaxMemoryUsage. Você pode especificar o número de megabytes (MB) ou usar o valor 0 para permitir que a transformação use uma quantidade dinâmica de memória com base nas suas necessidades e na memória física disponível. A propriedade personalizada MaxMemoryUsage pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
## Comparação de linhas  
 Quando você configura a transformação Agrupamento Difuso, é possível especificar o algoritmo de comparação que a transformação usa para comparar linhas na entrada de transformação. Se você definir a propriedade Exhaustive como **true**, a transformação comparará todas as linhas na entrada com todas as outras linhas na entrada. Esse algoritmo de comparação pode produzir resultados mais precisos, mas é provável que faça com que a transformação seja executada com mais lentidão, a menos que o número de linhas na entrada seja pequeno. Para evitar problemas no desempenho, é aconselhável definir a propriedade Exhaustive como **true** somente durante o desenvolvimento de pacote.  
  
## Tabelas e índices temporários  
 No tempo de execução, a transformação Agrupamento Difuso cria objetos temporários, como tabelas e índices, potencialmente de tamanho significante, no banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para que a transformação seja conectada. O tamanho das tabelas e índices é proporcional ao número de linhas na entrada de transformação e o número de tokens criados pela transformação Agrupamento Difuso.  
  
 A transformação também consulta as tabelas temporárias. Portanto, você deverá considerar conectar a transformação Agrupamento Difuso a uma instância de não produção do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especialmente se o servidor de produção tiver limitado o espaço em disco disponível.  
  
 O desempenho dessa transformação poderá melhorar se as tabelas e os índices que ele usa estiverem no computador local.  
  
## Configuração da transformação Agrupamento Difuso  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Agrupamento Difuso**, clique em um dos seguintes tópicos:  
  
-   [Editor de Transformação Agrupamento Difuso &#40;Guia Gerenciador de Conexões&#41;](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation-editor-connection-manager-tab.md)  
  
-   [Editor de Transformação Agrupamento Difuso &#40;Guia Colunas&#41;](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation-editor-columns-tab.md)  
  
-   [Editor de Transformação Agrupamento Difuso &#40;Guia Avançado&#41;](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation-editor-advanced-tab.md)  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../Topic/Common%20Properties.md)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## Tarefas relacionadas  
 Para obter detalhes sobre como definir as propriedades dessa tarefa, clique em um dos tópicos a seguir:  
  
-   [Identificar linhas de dados semelhantes por meio da transformação Agrupamento Difuso](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## Consulte também  
 [Transformação Pesquisa Difusa](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  