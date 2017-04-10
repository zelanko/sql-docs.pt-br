---
title: "Transforma&#231;&#227;o Pesquisa Difusa | Microsoft Docs"
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
  - "sql13.dts.designer.fuzzylookuptrans.f1"
helpviewer_keywords: 
  - "limpando dados"
  - "comparando dados"
  - "delimitadores de token [Integration Services]"
  - "índices temporários [Integration Services]"
  - "tabelas temporárias [Integration Services]"
  - "transformação Pesquisa Difusa"
  - "tabelas de referência [Integration Services]"
  - "corresponder dados similares [Integration Services]"
  - "substituindo valores ausentes"
  - "corrigindo dados [Integration Services]"
  - "cache [Integration Services]"
  - "padronizando dados [Integration Services]"
  - "pesquisas [Integration Services]"
  - "pontuações de confiança [Integration Services]"
  - "correspondências difusas"
  - "valores ausentes substituídos [Integration Services]"
  - "limites de similaridade [Integration Services]"
ms.assetid: 019db426-3de2-4ca9-8667-79fd9a47a068
caps.latest.revision: 75
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 75
---
# Transforma&#231;&#227;o Pesquisa Difusa
  A transformação Pesquisa Difusa executa tarefas de limpeza de dados, como padronização de dados, correção de dados e fornecimento de valores ausentes.  
  
> [!NOTE]  
>  Para obter informações mais detalhadas sobre a transformação Pesquisa Difusa, incluindo limitações de desempenho e de memória, consulte o white paper, [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](http://go.microsoft.com/fwlink/?LinkId=96604) (Pesquisa Difusa e Agrupamento Difuso no SQL Server Integration Services 2005).  
  
 A transformação Pesquisa Difusa difere da transformação Pesquisa no uso da correspondência difusa. A transformação Pesquisa usa uma junção por igualdade para localizar registros correspondentes na tabela de referência. Ela retorna registros com pelo menos um registro correspondente e retorna registros sem registros correspondentes. Por outro lado, a transformação Pesquisa Difusa usa a correspondência difusa para retornar uma ou mais correspondências aproximadas na tabela de referência.  
  
 A transformação Pesquisa Difusa frequentemente segue uma transformação Pesquisa em um fluxo de dados de pacote. Primeiro, a transformação Pesquisa tenta localizar uma correspondência exata. Se falhar, a transformação Pesquisa Difusa oferecerá correspondências próximas da tabela de referência.  
  
 A transformação precisa acessar uma fonte de dados de referência que contém os valores usados para limpar e ampliar os dados de entrada. A fonte de dados de referência deve ser uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . A correspondência entre o valor em uma coluna de entrada e o valor na tabela de referência pode ser uma correspondência exata ou difusa. Porém, a transformação exige pelo menos uma correspondência de coluna a ser configurada para correspondência difusa. Se quiser usar apenas a correspondência exata, use a transformação Pesquisa.  
  
 Essa transformação tem uma entrada e uma saída.  
  
 Apenas colunas com os tipos de dados **DT_WSTR** e **DT_STR** podem ser usadas na correspondência difusa. A correspondência exata pode usar qualquer tipo de dados DTS, exceto **DT_TEXT**, **DT_NTEXT** e **DT_IMAGE**. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md). Colunas que participam da junção entre a tabela de entrada e de referência deve ter tipos de dados compatíveis. Por exemplo, é válido para unir uma coluna com o tipo de dados DTS **DT_WSTR** a uma coluna com o tipo de dados **nvarchar** do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], mas inválido para unir uma coluna com o tipo de dados **DT_WSTR** a uma coluna com o tipo de dados **int**.  
  
 Você pode personalizar essa transformação especificando a quantidade máxima de memória, o algoritmo de comparação de linha e o cache de índices e tabelas de referência que a transformação usa.  
  
 A quantidade de memória que a transformação Pesquisa Difusa usa pode ser configurada definindo a propriedade personalizada MaxMemoryUsage. Você pode especificar o número de megabytes (MB) ou usar o valor 0 para permitir que a transformação use uma quantidade dinâmica de memória com base nas suas necessidades e na memória física disponível. A propriedade personalizada MaxMemoryUsage pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
## Controlando o comportamento da correspondência difusa  
 A transformação Pesquisa Difusa inclui três recursos para personalizar a pesquisa: número máximo de correspondências para retornar por linha de entrada, delimitadores de token e limites de similaridade.  
  
 A transformação retorna zero ou mais correspondências até o número de correspondências especificadas. A especificação de um número máximo de correspondências não garante que a transformação retorne o número máximo de correspondências; apenas garante que a transformação retorne no máximo o número de correspondências referido. Se você definir o número máximo de correspondências como um valor maior que 1, a saída da transformação poderá incluir mais de uma linha por pesquisa, e algumas das linhas podem ser duplicatas.  
  
 A transformação fornece um conjunto padrão de delimitadores para criar tokens de dados, mas você pode adicionar delimitadores de token que atendam às necessidades dos seus dados. A propriedade Delimiters contém os delimitadores padrão. O uso de token é importante porque define as unidades dentro dos dados, as quais são comparadas umas com as outras.  
  
 Os limites de similaridade podem ser definidos nos níveis de componente e de junção. O limite de similaridade relacionado à junção só está disponível quando a transformação executa uma correspondência difusa entre colunas na tabela de referência e de entrada. O intervalo de similaridade é de 0 a 1. Quanto mais próximo de 1 for o limite, mais similares as linhas e colunas devem ser para se qualificarem como duplicatas. Você especifica o limite de similaridade definindo a propriedade MinSimilarity nos níveis de componente e de junção. Para satisfazer a similaridade especificada no nível de componente, todas as linhas deverão ter uma similaridade em todas as correspondências que seja maior ou igual ao limite de similaridade especificado no nível de componente. Ou seja, você não pode especificar uma correspondência muito próxima no nível de componente, a menos que as correspondências relacionadas à linha ou à junção estejam igualmente próximas.  
  
 Cada correspondência inclui uma pontuação de similaridade e uma pontuação de confiança. A pontuação de similaridade é uma medida matemática de similaridade textural entre o registro de entrada e o registro que a transformação Pesquisa Difusa retorna da tabela de referência. A pontuação de confiança é uma medida que indica qual a probabilidade de um determinado valor ser a melhor correspondência entre as correspondências encontradas na tabela de referência. A pontuação de confiança atribuída a um registro depende dos outros registros correspondentes retornados. Por exemplo, a correspondência de *St.* e *Saint* retorna uma baixa pontuação de similaridade, independentemente de outras correspondências. Caso *Saint* seja a única correspondência retornada, a pontuação de confiança será alta. Caso *Saint* e *St.* sejam exibidos na tabela de referência, a confiança em *St.* será alta, e a confiança em *Saint* , baixa. Porém, a alta similaridade pode não significar confiança alta. Por exemplo, se você estiver pesquisando o valor *Chapter 4*, os resultados retornados *Chapter 1*, *Chapter 2*e *Chapter 3* terão uma pontuação de similaridade alta, mas uma baixa pontuação de confiança porque não está claro qual dos resultados é a melhor correspondência.  
  
 A pontuação de similaridade é representada por um valor decimal entre 0 e 1, em que uma pontuação de similaridade de 1 representa uma correspondência exata entre o valor na coluna de entrada e o valor na tabela de referência. A pontuação de confiança, também um valor decimal entre 0 e 1, indica a confiança na correspondência. Se não for encontrada nenhuma correspondência utilizável, as pontuações de similaridade e confiança iguais a 0 serão atribuídas à linha, e as colunas de saída copiadas da tabela de referência conterão valores nulos.  
  
 Às vezes, é possível que a Pesquisa Difusa não localize correspondências apropriadas na tabela de referência. Isso poderá acontecer se o valor de entrada usado em uma pesquisa for uma única palavra curta. Por exemplo, *helo* não tem correspondência com o valor *hello* em uma tabela de referência quando nenhum outro token está presente na coluna ou em qualquer outra coluna da linha.  
  
 As colunas de saída de transformação incluem as colunas de entrada marcadas como de passagem, as selecionadas na tabela de pesquisa e as seguintes colunas adicionais:  
  
-   **_Similarity**, uma coluna que descreve a similaridade entre valores nas colunas de entrada e de referência.  
  
-   **_Confidence**, uma coluna que descreve a qualidade da correspondência.  
  
 A transformação usa a conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para criar as tabelas temporárias usadas pelo algoritmo de correspondência difusa.  
  
## Executando a Transformação Pesquisa Difusa  
 Quando o pacote executar a transformação pela primeira vez, ela copiará a tabela de referência, adicionará uma chave com um tipo de dados de inteiro à tabela nova e criará um índice na coluna-chave. Em seguida, a transformação criará um índice, denominado índice de correspondência, na cópia da tabela de referência. O índice de correspondência armazena os resultados da criação de tokens dos valores nas colunas de entrada de transformação e, em seguida, a transformação usa os tokens na operação de pesquisa. O índice de correspondência é uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Quando o pacote for executado novamente, a transformação poderá usar um índice de correspondência existente ou criar um índice novo. Se a tabela de referência for estática, o pacote poderá evitar o processo potencialmente caro de recriar o índice para sessões repetidas de limpeza de dados. Se você optar por usar um índice existente, o índice será criado na primeira vez em que o pacote for executado. Se várias transformações de Pesquisa Difusa usarem a mesma tabela de referência, todas elas poderão usar o mesmo índice. Para usar novamente o índice, as operações de pesquisa devem ser idênticas; a pesquisa deve usar as mesmas colunas. Você pode nomear o índice e selecionar a conexão com o banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que salva o índice.  
  
 Se a transformação salvar o índice de correspondência, esse índice poderá ser mantido automaticamente. Isso significa que toda vez que um registro na tabela de referência for atualizado, o índice de correspondência será também atualizado. A manutenção do índice de correspondência pode poupar tempo de processamento porque o índice não precisa ser recriado quando o pacote é executado. Você pode especificar como a transformação gerencia o índice de correspondência.  
  
 A tabela a seguir descreve as opções de índice de correspondência.  
  
|Opção|Description|  
|------------|-----------------|  
|**GenerateAndMaintainNewIndex**|Cria um índice novo, salva-o e faz a sua manutenção. A transformação instala acionadores na tabela de referência para manter essa tabela de referência e a tabela de índice sincronizadas.|  
|**GenerateAndPersistNewIndex**|Cria um índice novo, salva-o, mas não faz a sua manutenção.|  
|**GenerateNewIndex**|Cria um índice novo, mas não o salva.|  
|**ReuseExistingIndex**|Reutiliza um índice existente.|  
  
### Manutenção da tabela de índices de correspondência  
 A opção **GenerateAndMaintainNewIndex** instala acionadores na tabela de referência para manter a tabela de índices de referência e a tabela de referência sincronizadas. Se você precisar remover o gatilho instalado, será preciso executar o procedimento armazenado **sp_FuzzyLookupTableMaintenanceUnInstall** e fornecer o nome especificado na propriedade MatchIndexName como o valor de parâmetro de entrada.  
  
 Não exclua a tabela de índices de correspondência mantida antes de executar o procedimento armazenado **sp_FuzzyLookupTableMaintenanceUnInstall**. Se a tabela de índices de correspondência for excluída, os acionadores na tabela de referência não serão executados corretamente. Todas as atualizações subsequentes da tabela de referência falharão até que você descarte manualmente os acionadores da tabela de referência.  
  
 O comando SQL TRUNCATE TABLE não chama os acionadores DELETE. Se o comando TRUNCATE TABLE for usado na tabela de referência, a tabela de referência e o índice de correspondência não serão mais sincronizados, e a transformação Pesquisa Difusa falhará. Visto que os acionadores que mantêm a tabela de índices de correspondência são instalados na tabela de referência, você deverá usar o comando SQL DELETE em vez do TRUNCATE TABLE.  
  
> [!NOTE]  
>  Quando você seleciona **Manter índice armazenado** na guia **Tabela de Referência** de **Editor de Transformação Pesquisa Difusa**, a transformação usa procedimentos armazenados gerenciados para manter o índice. Esses procedimentos armazenados gerenciados usam o recurso de integração de CLR (Common Language Runtime) no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por padrão, a integração de CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não está habilitada. Para usar a funcionalidade **Manter índice armazenado** , você deve habilitar a integração de CLR. Para obter mais informações, consulte [Enabling CLR Integration](../Topic/Enabling%20CLR%20Integration.md).  
>   
>  Como a opção **Manter índice armazenado** requer a integração CLR, esse recurso funciona apenas quando você seleciona uma tabela de referência em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em que a integração CLR está habilitada.  
  
## Comparação de linhas  
 Quando você configura a transformação Pesquisa Difusa, é possível especificar o algoritmo de comparação que a transformação usa para localizar registros correspondentes na tabela de referência. Se você definir a propriedade Exhaustive como **True**, a transformação comparará todas as linhas na entrada com todas as outras linhas na tabela de referência. Esse algoritmo de comparação pode produzir resultados mais precisos, mas é provável que faça com que a transformação seja executada com mais lentidão, a menos que o número de linhas na tabela de referência seja pequeno. Se a propriedade Exhaustive for definida como **True**, toda a tabela de referência será carregada na memória. Para evitar problemas de desempenho, é aconselhável definir a propriedade Exhaustive como **True** somente durante o desenvolvimento de pacote.  
  
 Se a propriedade Exhaustive for definida como **False**, a transformação Pesquisa Difusa retornará apenas as correspondências que têm, pelo menos, um token ou uma subcadeia de caracteres indexado (a subcadeia de caracteres é denominada *q-gram*) em comum com o registro de entrada. Para maximizar a eficiência das pesquisas, apenas um subconjunto dos tokens em cada linha da tabela é indexado na estrutura de índice invertida que a transformação Pesquisa Difusa usa para localizar correspondências. Quando o conjunto de dados de entrada for pequeno, você poderá definir Exhaustive como **True** a fim de evitar a perda de correspondências para as quais não haja tokens em comum na tabela de índice.  
  
## Cache de índices e tabelas de referência  
 Quando você configura a transformação Pesquisa Difusa, é possível especificar se a transformação deve armazenar parcialmente em cache o índice e a tabela de referência na memória antes de a transformação realizar o seu trabalho. Se a propriedade WarmCaches for definida como **True**, o índice e a tabela de referência serão carregados na memória. Quando a entrada tiver muitas linhas, defina a propriedade WarmCaches como **True** para melhorar o desempenho da transformação. Quando o número de linhas de entrada for pequeno, defina a propriedade WarmCaches como **False** para tornar mais rápida a reutilização de um índice grande.  
  
## Tabelas e índices temporários  
 Durante a execução, a transformação Pesquisa Difusa cria objetos temporários, como tabelas e índices, no banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a que a transformação se conecta. O tamanho dessas tabelas e índices temporários é proporcional ao número de linhas e tokens na tabela de referência e ao número de tokens que a transformação Pesquisa Difusa cria; por esse motivo, eles podem consumir uma grande quantidade de espaço em disco. A transformação também consulta as tabelas temporárias. Portanto, você deverá considerar a conexão da transformação Pesquisa Difusa a uma instância de não produção de um banco de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], especialmente se o servidor de produção tiver espaço em disco disponível limitado.  
  
 O desempenho dessa transformação poderá melhorar se as tabelas e os índices que ele usa estiverem no computador local. Se a tabela de referência que a transformação Pesquisa Difusa usar estiver no servidor de produção, considere copiar a tabela a um servidor de não produção e configurar a transformação Pesquisa Difusa para acessar a cópia. Com isso, impede-se que as consultas de pesquisa consumam recursos do servidor de produção. Além disso, se a transformação Pesquisa Difusa mantiver o índice de correspondência, ou seja, se MatchIndexOptions for definido como **GenerateAndMaintainNewIndex**, a transformação poderá bloquear a tabela de referência durante a operação de limpeza dos dados e impedir que outros usuários e aplicativos acessem essa tabela.  
  
## Configurando a transformação pesquisa difusa  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor de Transformação Pesquisa Difusa** , clique em um dos seguintes tópicos:  
  
-   [Editor de Transformação Pesquisa Difusa &#40;Guia Tabela de Referência&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-reference-table-tab.md)  
  
-   [Editor de Transformação Pesquisa Difusa &#40;guia Colunas&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-columns-tab.md)  
  
-   [Editor de Transformação Pesquisa Difusa &#40;Guia Avançado&#41;](../../../integration-services/data-flow/transformations/fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](../Topic/Common%20Properties.md)  
  
-   [Propriedades personalizadas de Transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## Tarefas relacionadas  
 Para obter detalhes sobre como definir as propriedades de um componente de fluxo de dados, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Consulte também  
 [Transformação Pesquisa](../../../integration-services/data-flow/transformations/lookup-transformation.md)   
 [Transformação Agrupamento Difuso](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  