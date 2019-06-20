---
title: Solucionar problemas de dados de processo (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 678f523c-e181-4456-9a54-7b7bf044b8d2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f76d67d5e44fc700d4b889840ef2dcc07a0bfde0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065764"
---
# <a name="troubleshoot-process-data-ssas-tabular"></a>Solucionar problemas de dados de processo (SSAS tabular)
  Este tópico fornece informações sobre como processar (atualizar) dados de modelo ao criar um modelo usando o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Este tópico não fornece informações sobre como processar dados em modelos que foram implantados em uma instância de servidor do Analysis Services. Para obter mais informações sobre processamento de dados em um modelo implantado, consulte [Script de tarefas administrativas no Analysis Services](script-administrative-tasks-in-analysis-services.md).  
  
 Seções neste tópico:  
  
-   [Como funciona o processamento de dados](#bkmk_how_df_works)  
  
-   [Impacto do processamento de dados](#bkmk_impact_of_df)  
  
-   [Determinando a fonte de dados](#bkmk_det_source)  
  
-   [Determinando quando os dados foram atualizados pela última vez](#bkmk_det_last_ref)  
  
-   [Restrições das fontes de dados atualizáveis](#bkmk_restrictions)  
  
-   [Restrições quanto a alterações feitas em uma fonte de dados](#bkmk_rest_changes)  
  
##  <a name="bkmk_how_df_works"></a> Como funciona o processamento de dados  
 Quando você processa os dados, os dados no designer de modelo são substituídos por novos dados. Não é possível importar apenas linhas de dados novas ou só de dados alterados. O designer de modelo não acompanha quais linhas foram adicionadas anteriormente.  
  
 O processamento dos dados ocorre como uma transação. Isso significa que, uma vez iniciada a atualização dos dados, toda a atualização falhará ou será bem-sucedida; você jamais terá dados parcialmente corretos.  
  
 O processo de dados manual, iniciada no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], é tratado pela instância de memória local do Analysis Services. Portanto, a operação de processamento dos dados pode afetar o desempenho de outras tarefas no computador. Porém, se você agendar o processo automático de dados em um modelo implantado usando um script, a instância do Analysis Services gerenciará o processo de importação e seu controle de tempo.  
  
##  <a name="bkmk_impact_of_df"></a> Impacto do processamento de dados  
 Um processo de dados normalmente dispara recálculo de dados.  O processamento de dados significa a obtenção dos mais recentes das origens externas; recalculando significa a atualização do resultado de todas as fórmulas que usam dados que foram alterados. Uma operação de processamento normalmente dispara o recálculo.  
  
 Portanto, você deve estar sempre atento ao impacto potencial antes de alterar as fontes de dados ou processar os dados obtidos na fonte de dados, além de considerar estas consequências em potencial:  
  
-   Algumas partes dos dados do modelo podem ser corrompidas devido a alterações feitas na fonte de dados. Se nem todas as colunas puderem ser recuperadas na fonte de dados (por exemplo, se elas foram excluídas ou alteradas), haverá falha no processo e você deverá atualizar os mapeamentos entre os dados de origem e os dados do modelo. Para obter mais informações, consulte [Edit an Existing Data Source Connection &#40;SSAS Tabular&#41;](edit-an-existing-data-source-connection-ssas-tabular.md).  
  
-   Após o processamento, algumas colunas podem ser sinalizadas por conterem um erro. Isso pode acontecer porque a fórmula da DAX na coluna usa dados que ficaram indisponíveis quando você os processou, o tipo de coluna foi alterado ou um valor inválido foi adicionado aos dados externos. Para resolver o problema, você poderá editar a fórmula ou excluir a coluna se for baseada em dados que não estão mais disponíveis.  
  
-   As fórmulas que usam os dados atualizados precisarão ser recalculadas. Dependendo do tamanho do modelo, isso pode demorar um pouco.  
  
-   Se o modelo contiver várias fontes de dados, você talvez precise processar todo o modelo (Processar Tudo), mesmo que apenas uma fonte de dados externa tenha sido alterada. Por exemplo, se você criar medidas que dependem de colunas calculadas, e essas colunas calculadas usarem valores de outras colunas calculadas, o designer de modelo primeiro analisará as dependências e, em seguida, processará a cadeia inteira de objetos relacionados na ordem. Dependendo da complexidade das dependências, isso pode demorar muito.  
  
-   Quando você altera um filtro, todo o modelo deve ser recalculado.  
  
##  <a name="bkmk_det_source"></a> Determinando a fonte de dados  
 Se você não tiver certeza da origem dos dados do modelo, poderá usar as ferramentas no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para obter os detalhes, inclusive o nome do arquivo de origem e o caminho.  
  
#### <a name="to-find-the-source-of-existing-data"></a>Para localizar a fonte de dados existente  
  
1.  No designer de modelo, selecione a tabela que contém os dados cuja origem você deseja conhecer.  
  
2.  Clique no menu **Tabela** e clique em **Propriedades da Tabela**.  
  
3.  Na caixa de diálogo **Editar Propriedades da Tabela** , anote o valor listado para **Nome da Conexão**.  
  
4.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Conexões Existentes**.  
  
5.  Na caixa de diálogo **Conexões Existentes** , selecione a fonte de dados que tem o nome que você encontrou na etapa 3 e clique em **Editar**.  
  
6.  Na caixa de diálogo **Editar Conexões** , exiba as informações da conexão, como o nome do banco de dados, o caminho do arquivo ou o caminho do relatório.  
  
##  <a name="bkmk_det_last_ref"></a> Determinando quando os dados foram atualizados pela última vez  
 É possível usar as Propriedades da Tabela para determinar quando os dados foram atualizados pela última vez.  
  
#### <a name="to-find-the-date-and-time-that-a-table-was-last-processed"></a>Para localizar a data e a hora do último processamento de uma tabela  
  
1.  No designer de modelo, selecione a tabela que contém os dados cuja data de atualização você deseja conhecer.  
  
2.  Clique no menu **Tabela** e clique em **Propriedades da Tabela**.  
  
3.  Na caixa de diálogo **Editar Propriedades da Tabela** , **Última Atualização** mostra a última data em que a tabela foi atualizada.  
  
##  <a name="bkmk_restrictions"></a> Restrições das fontes de dados atualizáveis  
 Algumas restrições aplicam-se às fontes de dados que podem ser processadas automaticamente de um modelo implantado em uma instância do Analysis Services. Selecione apenas as fontes de dados que atendam aos seguintes critérios:  
  
-   A fonte de dados deve estar disponível no momento em que ocorre o processo de dados e disponível no local indicado. Se a fonte de dados original estiver em uma unidade de disco local do usuário que criou o modelo, você deverá excluir essa fonte de dados da operação de processo de dados ou encontrar uma forma de publicar essa fonte de dados em um local acessível por uma conexão de rede. Se você mover uma fonte de dados para um local de rede, abra o modelo no designer de modelo e repita as etapas de recuperação de dados. Isso é necessário para restabelecer as informações da conexão armazenadas nas propriedades de conexão da fonte de dados.  
  
-   A fonte de dados precisa ser acessada através das credenciais inseridas na conexão de fonte de dados. As credenciais inseridas são criadas na conexão de fonte de dados quando você se conecta à fonte de dados externa.  
  
-   O processo de dados deve ter êxito para todas as fontes de dados especificadas. Caso contrário, os dados processados serão descartados e você ficará com a última versão salva do modelo. Exclua qualquer fonte de dados duvidosa.  
  
-   O processo de dados não deve invalidar outros dados em seu modelo. Quando você processa um subconjunto de seus dados, é importante compreender se o modelo ainda é válido quando dados mais novos são agregados com dados estáticos que são de períodos diferentes. Como um designer de modelo, cabe a você conhecer suas dependências de dados e garantir que o processo de dados seja apropriada para o próprio modelo.  
  
     Uma fonte de dados externa é acessada através de uma cadeia de conexão inserida, uma URL ou um caminho UNC que você especificou quando importou os dados originais para o modelo usando o Assistente de Importação de Tabela. As informações de conexão originais armazenadas na conexão de fonte de dados são reutilizadas nas operações de atualização de dados subsequentes. Não há informações de conexão separadas que sejam criadas e gerenciadas para fins de processo de dados; apenas as informações de conexão existentes são usadas.  
  
##  <a name="bkmk_rest_changes"></a> Restrições quanto a alterações feitas em uma fonte de dados  
 Há algumas restrições nas alterações que você pode fazer a uma fonte de dados:  
  
-   Os tipos de dados de uma coluna somente podem ser alterados para um tipo de dados compatível. Por exemplo, se os dados da coluna contiverem números decimais, você não poderá alterar o tipo de dados para inteiro. No entanto, você pode alterar os dados numéricos para texto. Para obter mais informações sobre tipos de dados, consulte [Tipos de dados com suporte &#40;SSAS de Tabela&#41;](tabular-models/data-types-supported-ssas-tabular.md).  
  
-   Não é possível selecionar várias colunas em tabelas diferentes e alterar as propriedades das colunas. Você pode trabalhar somente com uma tabela ou exibição de cada vez.  
  
## <a name="see-also"></a>Consulte também  
 [Processando os dados manualmente &#40;SSAS Tabular&#41;](manually-process-data-ssas-tabular.md)   
 [Editar uma conexão de fonte de dados existente &#40;SSAS Tabular&#41;](edit-an-existing-data-source-connection-ssas-tabular.md)  
  
  
