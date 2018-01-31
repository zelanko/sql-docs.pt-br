---
title: "Transformação Agrupamento Difuso | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.fuzzygroupingtrans.f1
- sql13.dts.designer.fuzzygroupingtransformation.connection.f1
- sql13.dts.designer.fuzzygroupingtransformation.columns.f1
- sql13.dts.designer.fuzzygroupingtransformation.advanced.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- Fuzzy Grouping transformation
- temporary tables [Integration Services]
- grouping data
- standardizing data [Integration Services]
- columns [Integration Services], standardizing
- similarity thresholds [Integration Services]
- data cleaning [Integration Services]
- duplicate data [Integration Services]
ms.assetid: e43f17bd-9d13-4a8f-9f29-cce44cac1025
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 03ffaa3d6dda388fc660feafc68a57fd8ce6346c
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="fuzzy-grouping-transformation"></a>transformação Agrupamento Difuso
  A transformação Agrupamento Difuso executa tarefas de limpeza de dados identificando linhas de dados que provavelmente sejam duplicatas e selecionando uma linha canônica de dados a ser usada na padronização dos dados.  
  
> [!NOTE]  
>  Para obter informações mais detalhadas sobre transformação de Agrupamento Difuso, incluindo limitações de desempenho e de memória, consulte o white paper, [Pesquisa Difusa e Agrupamento Difuso no SQL Server Integration Services 2005](http://go.microsoft.com/fwlink/?LinkId=96604).  
  
 A transformação Agrupamento Difuso requer uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para criar tabelas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] temporárias que o algoritmo de transformação necessita para executar seu trabalho. A conexão deve determinar um usuário que tenha permissão para criar tabelas no banco de dados.  
  
 Para configurar a transformação, você deve selecionar as colunas de entrada a serem usadas para identificar duplicatas e selecionar o tipo de correspondência – difusa ou exata – para cada coluna. A correspondência exata garante que somente as linhas com valores idênticos na coluna sejam agrupadas. A correspondência exata pode ser se aplicada a colunas de qualquer tipo de dados do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , exceto DT_TEXT, DT_NTEXT e DT_IMAGE. Uma correspondência difusa agrupa linhas que têm aproximadamente os mesmos valores. O método para correspondência aproximada de dados é baseado em uma pontuação de similaridade especificada pelo usuário. Só colunas com os  tipos de dados DT_WSTR e DT_STR podem ser usadas em correspondência difusa. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
 A saída de transformação inclui todas as colunas de entrada, uma ou mais colunas com dados padronizados, e uma coluna que contém a pontuação de similaridade. A pontuação é um valor decimal entre 0 e 1. A linha canônica tem a pontuação 1. Outras linhas do grupo difuso têm pontuações que indicam a qualidade da correspondência entre a linha e a linha canônica. Quanto mais próxima de 1 for a pontuação, mais próxima será a correspondência da fila com a fila canônica. Se o grupo difuso tiver linhas duplicatas exatas da linha canônica, essas linhas também receberão pontuação 1. A transformação não remove linhas duplicadas; ela as agrupa, criando uma chave que associa a linha canônica a linhas similares.  
  
 A transformação produz uma linha de saída para cada linha de entrada, com as seguintes colunas adicionais:  
  
-   **_key_in**, uma coluna que identifica exclusivamente cada linha.  
  
-   **_key_out**, uma coluna que identifica um grupo de linhas duplicadas. A coluna **_key_out** tem o valor da coluna **_key_in** na linha de dados canônica. Linhas com o mesmo valor em **_key_out** fazem parte do mesmo grupo. O valor **_key_out**de um grupo corresponde ao valor **_key_in** na linha de dados canônica.  
  
-   **_score**, um valor entre 0 e 1 que indica a semelhança da linha de entrada à linha canônica.  
  
 Esses são os nomes de coluna padrão e você pode configurar a transformação Agrupamento Difuso para usar outros nomes. A saída também fornece uma pontuação de similaridade para cada coluna que participa de um agrupamento difuso.  
  
 A transformação Agrupamento Difuso inclui dois recursos para personalizar o agrupamento que ela executa: delimitadores de token e limite de similaridade. A transformação fornece um conjunto padrão de delimitadores para criar tokens de dados, mas você pode adicionar novos delimitadores que melhoram essa criação.  
  
 O limite de similaridade indica como a transformação identifica rigidamente duplicatas. Os limites de similaridade podem ser definidos nos níveis de componente e de coluna. O limite de similaridade no nível de coluna só está disponível para as colunas que realizam a correspondência difusa. O intervalo de similaridade é de 0 a 1. Quanto mais próximo de 1 for o limite, mais similares as linhas e colunas devem ser para se qualificarem como duplicatas. Você especifica o limite de similaridade entre linhas e colunas definindo a propriedade MinSimilarity nos níveis de componente e coluna. Para satisfazer a similaridade que é especificada no nível de componente, todas as linhas devem ter uma similaridade por todas as colunas que seja maior ou igual ao limite de similaridade especificado no nível de componente.  
  
 A transformação Agrupamento Difuso calcula medidas internas de similaridade, e as linhas que são menos similares do que o valor especificado em MinSimilarity não são agrupados.  
  
 Para identificar um limite de similaridade que funcione para os seus dados, talvez seja preciso aplicar a transformação Agrupamento Difuso várias vezes usando limites de similaridade mínimos diferentes. No tempo de execução, as colunas de pontuação na saída de transformação contêm as pontuações de similaridade para cada linha do grupo. Você pode usar esses valores para identificar o limite de similaridade adequado para os seus dados. Se você quiser aumentar a similaridade, defina MinSimilarity como um valor maior que o valor nas colunas de pontuação.  
  
 Você pode personalizar o agrupamento que a transformação executa definindo as propriedades das colunas na entrada de transformação Agrupamento Difuso. Por exemplo, a propriedade FuzzyComparisonFlags especifica como a transformação compara os dados de cadeia de caracteres em uma coluna, e a propriedade ExactFuzzy especifica se a transformação executa uma correspondência difusa ou exata.  
  
 A quantidade de memória que a transformação Agrupamento Difuso usa pode ser configurada definindo a propriedade personalizada MaxMemoryUsage. Você pode especificar o número de megabytes (MB) ou usar o valor 0 para permitir que a transformação use uma quantidade dinâmica de memória com base nas suas necessidades e na memória física disponível. A propriedade personalizada MaxMemoryUsage pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Essa transformação tem uma entrada e uma saída. Não dá suporte a uma saída de erro.  
  
## <a name="row-comparison"></a>Comparação de linhas  
 Quando você configura a transformação Agrupamento Difuso, é possível especificar o algoritmo de comparação que a transformação usa para comparar linhas na entrada de transformação. Se você definir a propriedade Exhaustive como **true**, a transformação comparará todas as linhas na entrada com todas as outras linhas na entrada. Esse algoritmo de comparação pode produzir resultados mais precisos, mas é provável que faça com que a transformação seja executada com mais lentidão, a menos que o número de linhas na entrada seja pequeno. Para evitar problemas no desempenho, é aconselhável definir a propriedade Exhaustive como **true** somente durante o desenvolvimento de pacote.  
  
## <a name="temporary-tables-and-indexes"></a>Tabelas e índices temporários  
 No tempo de execução, a transformação Agrupamento Difuso cria objetos temporários, como tabelas e índices, potencialmente de tamanho significante, no banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para que a transformação seja conectada. O tamanho das tabelas e índices é proporcional ao número de linhas na entrada de transformação e o número de tokens criados pela transformação Agrupamento Difuso.  
  
 A transformação também consulta as tabelas temporárias. Portanto, você deverá considerar conectar a transformação Agrupamento Difuso a uma instância de não produção do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especialmente se o servidor de produção tiver limitado o espaço em disco disponível.  
  
 O desempenho dessa transformação poderá melhorar se as tabelas e os índices que ele usa estiverem no computador local.  
  
## <a name="configuration-of-the-fuzzy-grouping-transformation"></a>Configuração da transformação Agrupamento Difuso  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter detalhes sobre como definir as propriedades dessa tarefa, clique em um dos tópicos a seguir:  
  
-   [Identificar linhas de dados semelhantes por meio da transformação Agrupamento Difuso](../../../integration-services/data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
-   [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>Editor de Transformação Agrupamento Difuso (guia Gerenciador de Conexões)
  Use a guia **Gerenciador de Conexões** da caixa de diálogo **Editor de Transformação Agrupamento Difuso** para selecionar uma conexão existente ou criar uma nova.  
  
> [!NOTE]  
>  O servidor especificado pela conexão deve estar executando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A transformação Agrupamento Difuso cria objetos de dados temporários no tempdb que podem ser tão grandes quanto a entrada completa para a transformação. A execução da transformação emite, em seu decorrer, consultas de servidor contra esses objetos temporários. Isso pode afetar o desempenho global de servidor.  
  
### <a name="options"></a>Opções  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente usando a caixa de listagem ou crie uma nova conexão usando o botão **Novo** .  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
## <a name="fuzzy-grouping-transformation-editor-columns-tab"></a>Editor de Transformação Agrupamento Difuso (guia Colunas)
  Use a guia **Colunas** da caixa de diálogo **Editor de Transformação Agrupamento Difuso** para especificar as colunas usadas para agrupar linhas com valores duplicados.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Selecione nesta lista as colunas de entrada usadas para agrupar linhas com valores duplicados.  
  
 **Nome**  
 Visualize os nomes das colunas de entrada disponíveis.  
  
 **Passagem**  
 Selecione se a coluna de entrada deve ser incluída na saída da transformação. Todas as colunas usadas para agrupar são copiadas automaticamente para a saída. Você pode incluir colunas adicionais, marcando esta coluna.  
  
 **Coluna de Entrada**  
 Selecione uma das colunas de entrada selecionadas anteriormente na lista **Colunas de Entrada Disponíveis** .  
  
 **Alias de Saída**  
 Digite um nome descritivo para a coluna de saída correspondente. Por padrão, o nome da coluna de saída é idêntico ao nome da coluna de entrada.  
  
 **Alias de Saída de Grupo**  
 Digite um nome descritivo para a coluna que conterá o valor canônico para as duplicatas agrupadas. O nome padrão dessa coluna de saída é o nome da coluna de entrada acrescido de _clean.  
  
 **Associar Tipo**  
 Selecione correspondência difusa ou exata. As linhas serão consideradas duplicatas se forem suficientemente semelhantes em todas as colunas que têm tipo de correspondência difusa. Se você também especificar correspondência exata em certas colunas, apenas as linhas que contiverem valores idênticos nessas colunas serão consideradas possíveis duplicatas. Portanto, se souber que certa coluna não contém nenhum erro ou inconsistência, você poderá especificar correspondência exata nessa coluna para aumentar a exatidão da correspondência difusa nas outras colunas.  
  
 **Similaridade Mínima**  
 Defina o limite de similaridade no nível de junção, usando o controle deslizante. Quanto mais próximo de 1 for o valor, maior deverá ser a semelhança entre o valor de pesquisa e o valor da origem para a qualificação de correspondências. Aumentar o limite pode melhorar a velocidade de correspondência, já que menos registros serão considerados candidatos.  
  
 **Alias de Saída de Similaridade**  
 Especifique o nome da nova coluna de saída que conterá as pontuações de similaridade da junção selecionada. Se você deixar este valor vazio, a coluna de saída não será criada.  
  
 **Numerais**  
 Especifique a significância dos numerais à esquerda e à direita na comparação dos dados da coluna. Por exemplo, se os numerais à esquerda forem significativos, "123 Main Street" não será grupado com "456 Main Street".  
  
|Valor|Description|  
|-----------|-----------------|  
|**Nenhum**|Numerais à esquerda e à direita não são significativos.|  
|**À Esquerda**|Apenas numerais à esquerda são significativos.|  
|**À Direita**|Apenas numerais à direita são significativos.|  
|**À Esquerda e À Direita**|Numerais tanto à esquerda, quanto à direita são significativos.|  
  
 **Sinalizadores de Comparação**  
 Para obter mais informações sobre as opções de comparação de cadeias de caracteres, consulte [Comparando dados de cadeia de caracteres](../../../integration-services/data-flow/comparing-string-data.md).  
  
## <a name="fuzzy-grouping-transformation-editor-advanced-tab"></a>Editor de Transformação Agrupamento Difuso (guia Avançado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação Agrupamento Difuso** para especificar colunas de entrada e saída, definir limites de similaridade e definir delimitadores.  
  
> [!NOTE]  
>  As propriedades **Exhaustive** e **MaxMemoryUsage** da transformação Agrupamento Difuso não estão disponíveis no **Editor de Transformação Agrupamento Difuso**, mas podem ser definidas por meio do **Editor Avançado**. Para obter mais informações sobre essas propriedades, consulte a seção Transformação Agrupamento Difuso em [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
### <a name="options"></a>Opções  
 **Nome da coluna da chave de entrada**  
 Especifique o nome de uma coluna de saída que contém o identificador exclusivo para cada coluna de entrada. A coluna **_key_in** tem um valor que identifica exclusivamente cada linha.  
  
 **Nome da coluna da chave de saída**  
 Especifique o nome de uma coluna de saída que contém um identificador exclusivo para a linha canônica de um grupo de linhas duplicadas. A coluna **_key_out** corresponde ao valor **_key_in** da linha de dados canônica.  
  
 **Nome da coluna de pontuação de similaridade**  
 Especifique um nome para a coluna que contém a pontuação de similaridade. A pontuação de similaridade é um valor entre 0 e 1 que indica a similaridade da linha de entrada à linha canônica. Quanto mais próxima de 1 for a pontuação, mais próxima será a correspondência da fila com a fila canônica.  
  
 **Limite de similaridade**  
 Defina o limite de similaridade usando o controle deslizante. Quanto mais próximo de 1 for o limite, mais linhas deverão ser similares umas às outras para se qualificarem como duplicatas. Aumentar o limite pode melhorar a velocidade de correspondência, pois menos registros candidatos precisam ser considerados.  
  
 **Delimitadores de token**  
 A transformação fornece um conjunto padrão de delimitadores para criar tokens de dados, mas você pode adicionar ou remover delimitadores, conforme a necessidade, editando a lista.  
  
## <a name="see-also"></a>Consulte Também  
 [Transformação Pesquisa Difusa](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
