---
title: "Mesclar partições no Analysis Services (SSAS - Multidimensional) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- partitions [Analysis Services], merging
- merging partitions [Analysis Services]
ms.assetid: b3857b9b-de43-4911-989d-d14da0196f89
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4d4e5ae92e7352d3b7a37516d57bb34e70388542
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="merge-partitions-in-analysis-services-ssas---multidimensional"></a>Mesclar partições no Analysis Services (SSAS - Multidimensional)
  É possível mesclar partições em um banco de dados existente do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para consolidar dados de fatos de várias partições do mesmo grupo de medidas.  
  
 [Cenários comuns](#bkmk_Scenario)  
  
 [Requisitos](#bkmk_prereq)  
  
 [Atualizar a Fonte da Partição após mesclar partições](#bkmk_Where)  
  
 [Considerações especiais para partições segmentadas por tabela de fatos ou consulta nomeada](#bkmk_fact)  
  
 [Como mesclar partições usando o SSMS](#bkmk_partitionSSMS)  
  
 [Como mesclar partições usando o XMLA](#bkmk_partitionsXMLA)  
  
##  <a name="bkmk_Scenario"></a> Cenários comuns  
 A única configuração mais comum para o uso da partição envolve a separação dos dados na dimensão de tempo. A granularidade de tempo associada a cada partição varia de acordo com os requisitos empresariais específicos do projeto. Por exemplo, a segmentação pode ser feita por anos, com o ano mais recente dividido em meses, mais uma partição separada para o mês vigente. A partição do mês vigente usa regularmente novos dados.  
  
 Quando o mês vigente termina, a partição é mesclada novamente nos meses da partição até o momento atual e o processo continua. No final do ano, terá sido formada uma partição inteira de ano novo.  
  
 Como este cenário demonstra, a mesclagem de partições pode se tornar uma tarefa de rotina executada regularmente, fornecendo uma abordagem progressiva para consolidar e organizar dados históricos.  
  
##  <a name="bkmk_prereq"></a> Requisitos  
 As partições podem ser mescladas somente se satisfizerem todos os critérios a seguir:  
  
-   Elas têm o mesmo grupo de medidas.  
  
-   Elas têm a mesma estrutura.  
  
-   Elas devem estar em um estado processado.  
  
-   Elas têm os mesmos modos de armazenamento.  
  
-   Elas contêm projetos de agregação idênticos.  
  
-   Elas compartilham o mesmo nível de compatibilidade do repositório de cadeia de caracteres (se aplica somente aos grupos de medidas de contagem distinta particionada).  
  
 Se a partição de destino estiver vazia (isto é, ela tiver um design de agregação, mas nenhuma agregação), a mesclagem descartará as agregações para as partições de origem. Você deve executar Processar Índice, Processar Completo ou Processar Padrão na partição para criar as agregações.  
  
 As partições remotas podem ser mescladas apenas com outras partições remotas definidas com a mesma instância remota do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Se você estiver usando uma combinação de partições locais e remotas, uma abordagem alternativa é criar novas partições que incluam os dados combinados, excluindo as partições que não são mais usadas.  
  
 Para criar uma partição que possa ser mesclada no futuro, durante a criação da partição no Assistente para Partições, você pode optar por copiar o projeto de agregação de outras partições do cubo. Isso assegura que essas partições tenham o mesmo projeto de agregação. Ao serem mescladas, as agregações da partição de origem são combinadas com as agregações da partição de destino.  
  
##  <a name="bkmk_Where"></a> Atualizar a Fonte da Partição após mesclar partições  
 As partições são segmentadas por consulta, como a cláusula WHERE de uma consulta SQL usada para processar os dados, ou por uma tabela ou consulta nomeada que fornece dados à partição. A propriedade **Fonte** na partição indica se a partição está associada a uma consulta ou tabela.  
  
 Quando você mescla partições, o conteúdo das partições são consolidados, mas a propriedade **Fonte** não é atualizada para refletir o escopo adicional da partição. Isso significa que, se você reprocessar subsequentemente uma partição que mantém a **Fonte**original, obterá dados incorretos dessa partição. A partição agregará erroneamente dados no nível pai. O exemplo a seguir ilustra esse comportamento.  
  
 **O problema**  
  
 Suponha que você tenha um cubo que contém informações sobre três produtos de refrigerantes. Ele tem três partições que usam a mesma tabela de fatos. Essas partições são segmentadas por produto. A Partição 1 contém dados sobre [ColaFull], a Partição 2 contém dados sobre [ColaDecaf] e a Partição 3 contém dados sobre [ColaDiet]. Se a Partição 3 for mesclada na Partição 2, os dados da partição resultante (Partição 2) estarão corretos e os dados do cubo serão precisos. No entanto, quando a Partição 2 é processada, seu conteúdo pode ser determinado pelo pai dos membros no nível de produto. Esse pai, [SoftDrinks], também inclui [ColaFull], o produto da Partição 1. O processamento da Partição 2 carrega a partição com dados de todos os refrigerantes, incluindo [ColaFull]. Desse modo, o cubo contém dados duplicados para [ColaFull] e retorna dados incorretos para os usuários finais.  
  
 **A solução**  
  
 A solução é atualizar a propriedade **Fonte** , ajustando a cláusula WHERE ou a consulta nomeada, ou mesclando manualmente dados das tabelas de fatos subjacentes, para garantir que o processamento subsequente receba com precisão o escopo expandido da partição.  
  
 Nesse exemplo, após mesclar a Partição 3 na Partição 2, é possível fornecer um filtro como ("Product" = 'ColaDecaf' OR "Product" = 'ColaDiet') na Partição 2 resultante para especificar que apenas os dados sobre [ColaDecaf] e [ColaDiet] serão extraídos da tabela de fatos e que os dados que pertencem a [ColaFull] serão excluídos. Se preferir, especifique filtros para a Partição 2 e a Partição 3 quando forem criadas; esses filtros serão combinados durante o processo de mesclagem. De qualquer modo, depois que a partição for processada, o cubo não vai conter dados duplicados.  
  
 **A conclusão**  
  
 Após mesclar partições, sempre verifique **Fonte** para saber se o filtro está correto para os dados mesclados. Se você tiver iniciado com uma partição que incluía os dados históricos para Q1, Q2 e Q3, e agora mesclar Q4, ajuste o filtro para incluir Q4. Caso contrário, o processamento subsequente da partição gerará resultados incorretos. Ele não estará correto para Q4.  
  
##  <a name="bkmk_fact"></a> Considerações especiais para partições segmentadas por tabela de fatos ou consulta nomeada  
 Além das consultas, as partições também podem ser segmentadas por tabela ou consulta nomeada. Se as partições de origem e de destino usam a mesma tabela de fatos em uma fonte de dados ou exibição da fonte de dados, a propriedade **Fonte** é válida após mesclar partições. Ela especifica os dados da tabela de fatos que são apropriadas para a partição resultante. Como os fatos necessários para a partição resultante estão presentes na tabela de fatos, não é necessário fazer modificações na propriedade **Fonte** .  
  
 As partições que usam dados de várias tabelas de fatos ou consultas nomeadas exigem trabalho adicional. Você deve mesclar manualmente os fatos da tabela da partição de origem na tabela da partição de destino.  
  
 Se preferir, altere a origem da partição mesclada para uma consulta nomeada que retorna o conteúdo separado das duas tabelas de fatos. Se essa etapa manual não for executada, a tabela de fatos não conterá informações completas.  
  
 Pela mesma razão, as partições que obtêm dados segmentados de consultas nomeadas também exigem atualização. A partição combinada agora deve ter uma consulta nomeada que retorna o conjunto de resultados combinados que foi obtido anteriormente em consultas nomeadas separadas.  
  
## <a name="partition-storage-considerations-molap"></a>Considerações de armazenamento de partição: MOLAP  
 Quando partições MOLAP são mescladas, os fatos armazenados nas estruturas multidimensionais das partições também são mesclados. Isso resulta em uma partição internamente completa e consistente. No entanto, os fatos armazenados em partições MOLAP são cópias de fatos da tabela. Quando a partição é processada posteriormente, os fatos da estrutura multidimensional são excluídos (somente para atualização) e os dados são copiados da tabela de fatos conforme especificado pela fonte de dados e pelo filtro da partição. Se a partição de origem usar uma tabela de fatos diferentes da partição de destino, a tabela da partição de origem deve ser mesclada manualmente com a tabela de fatos da partição de destino para garantir que um conjunto completo de dados esteja disponível para o processamento da partição resultante. Isto também se aplica se duas partições forem baseadas em consultas nomeadas diferentes.  
  
> [!IMPORTANT]  
>  Uma partição MOLAP mesclada com uma tabela de fatos incompleta contém uma cópia mesclada internamente dos dados da tabela de dados e é operada corretamente até ser processada.  
  
## <a name="partition-storage-considerations-holap-and-rolap-partitions"></a>Considerações de armazenamento de partição: partições HOLAP e ROLAP  
 Quando as partições HOLAP ou OLAP com tabelas de fatos diferentes são mescladas, essas tabelas não são mescladas automaticamente. A não ser que sejam mescladas manualmente, somente a tabela de fatos associada à partição de destino estará disponível na partição resultante. Os fatos associados à partição de origem não estão disponíveis para extração de detalhes na partição resultante e, quando a partição é processada, as agregações não resumem os dados da tabela não disponível.  
  
> [!IMPORTANT]  
>  Uma partição HOLAP ou ROLAP mesclada com uma tabela de fatos incompleta contém agregações precisas, mas fatos incompletos. As consultas que fazem referência aos fatos ausentes retornam dados incorretos. Quando a partição é processada, somente as agregações de fatos disponíveis são calculadas.  
  
 A ausência de fatos indisponíveis talvez não seja percebida, a não ser que um usuário tente extrair detalhes de um fato da tabela não disponível ou execute uma consulta que exija um fato dessa tabela. Como as agregações são combinadas durante o processo de mesclagem, as consultas cujos resultados baseiam-se apenas em agregações retornam dados imprecisos, embora outras consultas também possam retornar dados imprecisos. Mesmo após o processamento da partição resultante, os dados ausentes da tabela de fatos indisponível podem não ser percebidos, especialmente se representarem apenas uma pequena parte dos dados combinados.  
  
 As tabelas de fatos podem ser mescladas antes ou depois da mesclagem das partições. No entanto, as agregações não representarão os fatos subjacentes com precisão até que as duas operações tenham sido concluídas. É recomendado mesclar as partições HOLAP ou ROLAP que acessam tabelas de fatos diferentes quando os usuários não estiverem conectados ao cubo que contém essas partições.  
  
##  <a name="bkmk_partitionSSMS"></a> Como mesclar partições usando o SSMS  
  
> [!IMPORTANT]  
>  Antes de mesclar partições, primeiro copie as informações de filtro de dados (normalmente, a cláusula WHERE para filtros baseados em consultas SQL). Após a conclusão da mesclagem, atualize a propriedade Origem da Partição da partição que contém os dados de fatos acumulados.  
  
1.  No Pesquisador de Objetos, expanda o nó **Grupos de Medidas** do cubo que contém as partições que você deseja mesclar, expanda **Partições**, clique com o botão direito do mouse na partição que é o destino da operação de mesclagem. Por exemplo, se você estiver movendo dados de fatos trimestrais para uma partição que armazena dados de fatos anuais, selecione a partição que contém os dados de fatos anuais.  
  
2.  Clique em **mesclar partições** para abrir o **Mesclar partição \<nome da partição >** caixa de diálogo.  
  
3.  Em **Partições de Origem**, marque a caixa de seleção ao lado de cada partição de origem a ser mesclada com a partição de destino e clique em **OK**.  
  
    > [!NOTE]  
    >  As partições de origem são excluídas assim que a origem é mesclada na partição de destino. A atualização da pasta Partições para atualizar seu conteúdo após a mesclagem foi concluída.  
  
4.  Clique com o botão direito do mouse na partição que contém os dados acumulados e selecione **Propriedades**.  
  
5.  Abra a propriedade **Origem** e modifique a cláusula WHERE de modo que ela inclua os dados de partição recém-mesclados. Lembre-se de que a propriedade **Origem** não é atualizada automaticamente. Se você reprocessar sem primeiro atualizar **Origem**, talvez não obtenha todos os dados esperados.  
  
##  <a name="bkmk_partitionsXMLA"></a> Como mesclar partições usando o XMLA  
 Consulte este tópico para obter informações, [Mesclando partições &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md).  
  
## <a name="see-also"></a>Consulte também  
 [Processando objetos do Analysis Services](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)   
 [Partições &#40;Analysis Services – Dados Multidimensionais&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Criar e gerenciar uma partição local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)   
 [Criar e gerenciar uma partição remota &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [Definir o write-back de partição](../../analysis-services/multidimensional-models/set-partition-writeback.md)   
 [Partições habilitadas para gravação](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-write-enabled-partitions.md)   
 [Configurar armazenamento de cadeia de caracteres para dimensões e partições](../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md)  
  
  
