---
title: "Transformação pesquisa difusa | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.fuzzylookuptrans.f1
- sql13.dts.designer.fuzzylookuptransformation.referencetable.f1
- sql13.dts.designer.fuzzylookuptransformation.columns.f1
- sql13.dts.designer.fuzzylookuptransformation.advanced.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- temporary tables [Integration Services]
- Fuzzy Lookup transformation
- reference tables [Integration Services]
- match similar data [Integration Services]
- replacing missing values
- correcting data [Integration Services]
- cache [Integration Services]
- standardizing data [Integration Services]
- lookups [Integration Services]
- confidence scores [Integration Services]
- fuzzy matches
- missing values replaced [Integration Services]
- similarity thresholds [Integration Services]
ms.assetid: 019db426-3de2-4ca9-8667-79fd9a47a068
caps.latest.revision: 75
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4b557efa62075f7b88e6b70cf5950546444b95d8
ms.openlocfilehash: ff5f003749572b16e750b5940cd0f05b0b879fda
ms.contentlocale: pt-br
ms.lasthandoff: 08/19/2017

---
# <a name="fuzzy-lookup-transformation"></a>transformação Pesquisa Difusa
  A transformação Pesquisa Difusa executa tarefas de limpeza de dados, como padronização de dados, correção de dados e fornecimento de valores ausentes.  
  
> [!NOTE]  
>  Para obter informações mais detalhadas sobre a transformação Pesquisa Difusa, incluindo limitações de desempenho e de memória, consulte o white paper, [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](http://go.microsoft.com/fwlink/?LinkId=96604)(Pesquisa Difusa e Agrupamento Difuso no SQL Server Integration Services 2005).  
  
 A transformação Pesquisa Difusa difere da transformação Pesquisa no uso da correspondência difusa. A transformação Pesquisa usa uma junção por igualdade para localizar registros correspondentes na tabela de referência. Ela retorna registros com pelo menos um registro correspondente e retorna registros sem registros correspondentes. Por outro lado, a transformação Pesquisa Difusa usa a correspondência difusa para retornar uma ou mais correspondências aproximadas na tabela de referência.  
  
 A transformação Pesquisa Difusa frequentemente segue uma transformação Pesquisa em um fluxo de dados de pacote. Primeiro, a transformação Pesquisa tenta localizar uma correspondência exata. Se falhar, a transformação Pesquisa Difusa oferecerá correspondências próximas da tabela de referência.  
  
 A transformação precisa acessar uma fonte de dados de referência que contém os valores usados para limpar e ampliar os dados de entrada. A fonte de dados de referência deve ser uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . A correspondência entre o valor em uma coluna de entrada e o valor na tabela de referência pode ser uma correspondência exata ou difusa. Porém, a transformação exige pelo menos uma correspondência de coluna a ser configurada para correspondência difusa. Se quiser usar apenas a correspondência exata, use a transformação Pesquisa.  
  
 Essa transformação tem uma entrada e uma saída.  
  
 Apenas colunas com os tipos de dados **DT_WSTR** e **DT_STR** podem ser usadas na correspondência difusa. A correspondência exata pode usar qualquer tipo de dados DTS, exceto **DT_TEXT**, **DT_NTEXT**e **DT_IMAGE**. Para obter mais informações, consulte [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md). Colunas que participam da junção entre a tabela de entrada e de referência deve ter tipos de dados compatíveis. Por exemplo, é válido para unir uma coluna com o tipo de dados DTS **DT_WSTR** a uma coluna com o tipo de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **do** , mas inválido para unir uma coluna com o tipo de dados **DT_WSTR** a uma coluna com o tipo de dados **int** .  
  
 Você pode personalizar essa transformação especificando a quantidade máxima de memória, o algoritmo de comparação de linha e o cache de índices e tabelas de referência que a transformação usa.  
  
 A quantidade de memória que a transformação Pesquisa Difusa usa pode ser configurada definindo a propriedade personalizada MaxMemoryUsage. Você pode especificar o número de megabytes (MB) ou usar o valor 0 para permitir que a transformação use uma quantidade dinâmica de memória com base nas suas necessidades e na memória física disponível. A propriedade personalizada MaxMemoryUsage pode ser atualizada por uma expressão de propriedade quando o pacote é carregado. Para obter mais informações, consulte [Expressões do Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expressões de propriedade em pacotes](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
## <a name="controlling-fuzzy-matching-behavior"></a>Controlando o comportamento da correspondência difusa  
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
  
## <a name="running-the-fuzzy-lookup-transformation"></a>Executando a Transformação Pesquisa Difusa  
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
  
### <a name="maintenance-of-the-match-index-table"></a>Manutenção da tabela de índices de correspondência  
 A opção **GenerateAndMaintainNewIndex** instala acionadores na tabela de referência para manter a tabela de índices de referência e a tabela de referência sincronizadas. Se você precisar remover o gatilho instalado, será preciso executar o procedimento armazenado **sp_FuzzyLookupTableMaintenanceUnInstall** e fornecer o nome especificado na propriedade MatchIndexName como o valor de parâmetro de entrada.  
  
 Não exclua a tabela de índices de correspondência mantida antes de executar o procedimento armazenado **sp_FuzzyLookupTableMaintenanceUnInstall** . Se a tabela de índices de correspondência for excluída, os acionadores na tabela de referência não serão executados corretamente. Todas as atualizações subsequentes da tabela de referência falharão até que você descarte manualmente os acionadores da tabela de referência.  
  
 O comando SQL TRUNCATE TABLE não chama os acionadores DELETE. Se o comando TRUNCATE TABLE for usado na tabela de referência, a tabela de referência e o índice de correspondência não serão mais sincronizados, e a transformação Pesquisa Difusa falhará. Visto que os acionadores que mantêm a tabela de índices de correspondência são instalados na tabela de referência, você deverá usar o comando SQL DELETE em vez do TRUNCATE TABLE.  
  
> [!NOTE]  
>  Quando você seleciona **Manter índice armazenado** na guia **Tabela de Referência** de **Editor de Transformação Pesquisa Difusa**, a transformação usa procedimentos armazenados gerenciados para manter o índice. Esses procedimentos armazenados gerenciados usam o recurso de integração de CLR (Common Language Runtime) no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por padrão, a integração de CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não está habilitada. Para usar a funcionalidade **Manter índice armazenado** , você deve habilitar a integração de CLR. Para obter mais informações, consulte [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md).  
>   
>  Como a opção **Manter índice armazenado** requer a integração CLR, esse recurso funciona apenas quando você seleciona uma tabela de referência em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em que a integração CLR está habilitada.  
  
## <a name="row-comparison"></a>Comparação de linhas  
 Quando você configura a transformação Pesquisa Difusa, é possível especificar o algoritmo de comparação que a transformação usa para localizar registros correspondentes na tabela de referência. Se você definir a propriedade Exhaustive como **True**, a transformação comparará todas as linhas na entrada com todas as outras linhas na tabela de referência. Esse algoritmo de comparação pode produzir resultados mais precisos, mas é provável que faça com que a transformação seja executada com mais lentidão, a menos que o número de linhas na tabela de referência seja pequeno. Se a propriedade Exhaustive for definida como **True**, toda a tabela de referência será carregada na memória. Para evitar problemas de desempenho, é aconselhável definir a propriedade Exhaustive como **True** somente durante o desenvolvimento de pacote.  
  
 Se a propriedade Exhaustive for definida como **False**, a transformação Pesquisa Difusa retornará apenas as correspondências que têm, pelo menos, um token ou uma subcadeia de caracteres indexado (a subcadeia de caracteres é denominada *q-gram*) em comum com o registro de entrada. Para maximizar a eficiência das pesquisas, apenas um subconjunto dos tokens em cada linha da tabela é indexado na estrutura de índice invertida que a transformação Pesquisa Difusa usa para localizar correspondências. Quando o conjunto de dados de entrada for pequeno, você poderá definir Exhaustive como **True** a fim de evitar a perda de correspondências para as quais não haja tokens em comum na tabela de índice.  
  
## <a name="caching-of-indexes-and-reference-tables"></a>Cache de índices e tabelas de referência  
 Quando você configura a transformação Pesquisa Difusa, é possível especificar se a transformação deve armazenar parcialmente em cache o índice e a tabela de referência na memória antes de a transformação realizar o seu trabalho. Se a propriedade WarmCaches for definida como **True**, o índice e a tabela de referência serão carregados na memória. Quando a entrada tiver muitas linhas, defina a propriedade WarmCaches como **True** para melhorar o desempenho da transformação. Quando o número de linhas de entrada for pequeno, defina a propriedade WarmCaches como **False** para tornar mais rápida a reutilização de um índice grande.  
  
## <a name="temporary-tables-and-indexes"></a>Tabelas e índices temporários  
 Durante a execução, a transformação Pesquisa Difusa cria objetos temporários, como tabelas e índices, no banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a que a transformação se conecta. O tamanho dessas tabelas e índices temporários é proporcional ao número de linhas e tokens na tabela de referência e ao número de tokens que a transformação Pesquisa Difusa cria; por esse motivo, eles podem consumir uma grande quantidade de espaço em disco. A transformação também consulta as tabelas temporárias. Portanto, você deverá considerar a conexão da transformação Pesquisa Difusa a uma instância de não produção de um banco de dados [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , especialmente se o servidor de produção tiver espaço em disco disponível limitado.  
  
 O desempenho dessa transformação poderá melhorar se as tabelas e os índices que ele usa estiverem no computador local. Se a tabela de referência que a transformação Pesquisa Difusa usar estiver no servidor de produção, considere copiar a tabela a um servidor de não produção e configurar a transformação Pesquisa Difusa para acessar a cópia. Com isso, impede-se que as consultas de pesquisa consumam recursos do servidor de produção. Além disso, se a transformação Pesquisa Difusa mantiver o índice de correspondência, ou seja, se MatchIndexOptions for definido como **GenerateAndMaintainNewIndex**, a transformação poderá bloquear a tabela de referência durante a operação de limpeza dos dados e impedir que outros usuários e aplicativos acessem essa tabela.  
  
## <a name="configuring-the-fuzzy-lookup-transformation"></a>Configurando a transformação pesquisa difusa  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo **Editor Avançado** ou programaticamente, clique em um dos seguintes tópicos:  
  
-   [Propriedades comuns](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propriedades personalizadas da transformação](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Para obter detalhes sobre como definir as propriedades de um componente de fluxo de dados, consulte [Definir as propriedades de um componente de fluxo de dados](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="fuzzy-lookup-transformation-editor-reference-table-tab"></a>Editor de Transformação Pesquisa Difusa (guia Tabela de Referência)
  Use a guia **Tabela de Referência** da caixa de diálogo **Editor de Transformação Pesquisa Difusa** para especificar a tabela de origem e o índice a ser usado na pesquisa. A fonte de dados de referência deve ser uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  A transformação Pesquisa Difusa cria uma cópia de trabalho da tabela de referência. Os índices descritos abaixo são criados nesta tabela de trabalho usando uma tabela especial, não um índice do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] comum. A transformação não modifica as tabelas de origem existentes a menos que você selecione **Manter índice armazenado**. Nesse caso, ela cria um gatilho na tabela de referência que atualiza a tabela de trabalho e a tabela de índices de pesquisa baseada em alterações na tabela de referência.  
  
> [!NOTE]  
>  As propriedades **Exhaustive** e **MaxMemoryUsage** da transformação Pesquisa Difusa não estão disponíveis no **Editor de Transformação Pesquisa Difusa**, mas podem ser definidas por meio do **Editor Avançado**. Além disso, um valor acima de 100 para **MaxOutputMatchesPerInput** só pode ser especificado no **Editor Avançado**. Para obter mais informações sobre estas propriedades, consulte a seção Transformação de Pesquisa Difusa em [Transformation Custom Properties](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
### <a name="options"></a>Opções  
 **gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente na lista ou crie uma nova conexão clicando em **Nova**.  
  
 **Nova**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Gerar novo índice**  
 Especifique que a transformação deve criar um índice novo para ser utilizado na pesquisa.  
  
 **Nome da tabela de referência**  
 Selecione a tabela existente para usar como tabela de referência (pesquisa).  
  
 **Armazenar novo índice**  
 Selecione esta opção para salvar o novo índice de pesquisa.  
  
 **Novo nome de índice**  
 Se você optou por salvar o novo índice de pesquisa, digite um nome descritivo para o índice.  
  
 **Manter índice armazenado**  
 Se você optou por salvar o novo índice de pesquisa, especifique se deseja que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mantenha o índice.  
  
> [!NOTE]  
>  Quando você seleciona **Manter índice armazenado** na guia **Tabela de Referência** de **Editor de Transformação Pesquisa Difusa**, a transformação usa procedimentos armazenados gerenciados para manter o índice. Esses procedimentos armazenados gerenciados usam o recurso de integração de CLR (Common Language Runtime) no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por padrão, a integração de CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não está habilitada. Para usar a funcionalidade **Manter índice armazenado** , você deve habilitar a integração de CLR. Para obter mais informações, consulte [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md).  
>   
>  Como a opção **Manter índice armazenado** requer a integração CLR, esse recurso só funciona quando você seleciona uma tabela de referência em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] onde a integração CLR está habilitada.  
  
 **Usar índice já existente**  
 Especifique que a transformação deve usar um índice existente na pesquisa.  
  
 **Nome de um índice já existente**  
 Selecione um índice de pesquisa criado anteriormente na lista.  
  
## <a name="fuzzy-lookup-transformation-editor-columns-tab"></a>Editor de Transformação Pesquisa Difusa (guia Colunas)
  Use a guia **Colunas** da caixa de diálogo **Editor de Transformação Pesquisa Difusa** para definir propriedades das colunas de entrada e saída.  
  
### <a name="options"></a>Opções  
 **Colunas de Entrada Disponíveis**  
 Arraste colunas de entrada para conectá-las com colunas de pesquisa disponíveis. Essas colunas devem ter tipos de dados correspondentes com suporte. Selecione uma linha de mapeamento e clique com o botão direito do mouse para editar os mapeamentos na caixa de diálogo [Criar Relações](../../../integration-services/data-flow/transformations/create-relationships.md) .  
  
 **Nome**  
 Exiba os nomes das colunas de entrada disponíveis.  
  
 **Passagem**  
 Especifique se as colunas de entrada devem ser incluídas na saída da transformação.  
  
 **Colunas de Pesquisa Disponíveis**  
 Use as caixas de seleção para selecionar colunas nas quais executar operações de pesquisa difusa.  
  
 **coluna de pesquisa**  
 Selecione colunas de pesquisa na lista de colunas da tabela de referência disponíveis. Suas seleções se refletem nas da caixa de seleção da tabela **Colunas de Pesquisa Disponíveis** . Selecionar uma coluna na tabela **Colunas de Pesquisa Disponíveis** cria uma coluna de saída que contém o valor da coluna da tabela de referência para cada linha correspondente retornada.  
  
 **Alias de Saída**  
 Digite um alias para a saída de cada coluna de pesquisa. O padrão é o nome da coluna de pesquisa com um valor de índice numérico anexado; contudo, é possível escolher qualquer nome descritivo exclusivo.  
  
## <a name="fuzzy-lookup-transformation-editor-advanced-tab"></a>Editor de Transformação Pesquisa Difusa (guia Avançado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação Pesquisa Difusa** para definir parâmetros para a pesquisa difusa.  
  
### <a name="options"></a>Opções  
 **Número máximo de correspondências a produzir por pesquisa**  
 Especifique o número máximo de correspondências que a transformação pode retornar para cada linha de entrada. O padrão é **1**.  
  
 **Limite de similaridade**  
 Defina o limite de similaridade no nível de componente usando o controle deslizante. Quanto mais próximo de 1 for o valor, maior deverá ser a semelhança entre o valor de pesquisa e o valor da origem para a qualificação de correspondências. Aumentar o limite pode melhorar a velocidade de correspondência, já que menos registros serão considerados candidatos.  
  
 **Delimitadores de token**  
 Especifique os delimitadores usados pela transformação para criar tokens de valores de coluna.  
  
## <a name="see-also"></a>Consulte também  
 [Transformação Pesquisa](../../../integration-services/data-flow/transformations/lookup-transformation.md)   
 [Transformação agrupamento difuso](../../../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md)   
 [Transformações do Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
