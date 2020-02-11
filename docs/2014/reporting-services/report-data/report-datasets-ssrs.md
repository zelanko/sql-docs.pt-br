---
title: Adicionar dados a um relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f2e42303-e355-4c1f-bb3b-3338fbdd230d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 019ca09c83b0b3011e9940d9a4c988ce223e192f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107118"
---
# <a name="add-data-to-a-report-report-builder-and-ssrs"></a>Adicionar dados a um relatório (Construtor de Relatórios e SSRS)
  Para adicionar dados a um relatório, você cria conjuntos de dados. Cada conjunto de dados representa o conjunto de resultados gerado pela execução de um comando de consulta em uma fonte dados. As colunas do conjunto de resultados são a coleção de campos. As linhas do conjunto de resultados são os dados. O conjunto de resultados não contêm os dados reais. Um conjunto de dados contém as informações necessárias para recuperar um conjunto específico de dados de uma fonte de dados.  
  
 Há dois tipos de conjuntos de dados: inserido ou compartilhado. Um conjunto de dados inserido é definido em um relatório e usado apenas por esse relatório. Um conjunto de dados compartilhado é definido no servidor de relatório ou em um site do SharePoint e pode ser usado por vários relatórios. No Construtor de Relatórios, você pode criar conjuntos de dados compartilhados no modo Conjunto de Dados Compartilhado ou conjuntos de dados inseridos no modo Designer de Relatórios. No Designer de Relatórios do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode criar conjuntos de dados compartilhados como parte de um projeto ou conjuntos de dados inseridos como parte de um relatório.  
  
-   **Conjuntos de valores inseridos.** Diferente de aplicativos como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel, em que você trabalha diretamente com dados em uma planilha, no Construtor de Relatórios ou no Designer de Relatórios, você trabalha com metadados que representam os dados a serem recuperados quando o relatório for processado. Para criar um conjunto de dados inserido, selecione a fonte de dados e especifique uma consulta. Depois que você criar um conjunto de dados, use o painel Dados do Relatório para exibir a coleção de campos. Você pode exibir dados de um conjunto de dados em uma região de dados, como uma tabela ou gráfico. Em cada região de dados, é possível agrupar, filtrar e classificar os dados para organizá-los. Depois de criar o layout de relatório, execute o relatório para ver os dados reais.  
  
     Na figura a seguir, o painel Dados do Relatório exibe uma fonte de dados denominada [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)], um conjunto de dados denominado DataSet1 e cinco campos da coleção de campos do conjunto de dados. O painel Layout mostra uma tabela com a linha superior de títulos de coluna e a linha inferior com células de tabela que contêm texto. O texto do espaço reservado [Nome] contém metadados para o nome do campo. Quando o relatório é executado, o texto do espaço reservado é substituído pelos valores de dados reais. A tabela é expandida conforme necessário para exibir todos os dados.  
  
     ![rs_DataDesignandPreview](../media/rs-datadesignandpreview.gif "rs_DataDesignandPreview")  
  
-   **Conjuntos de valores compartilhados.** Crie um conjunto de dados compartilhado quando desejar usar um conjunto de dados em mais de um relatório. Para criar e salvar um conjunto de dados em um servidor de relatório ou em um site do SharePoint, use o Construtor de Relatórios na exibição de design do conjunto de dados compartilhado. Para criar um conjunto de dados compartilhado como parte de um projeto que pode ser implantado em um servidor ou site, use o Designer de Relatórios.  
  
     A ilustração a seguir mostra a exibição de Design do Conjunto de Dados Compartilhado no Construtor de Relatórios. Você pode selecionar ou modificar a conexão de dados, as propriedades de conjunto de dados, a consulta e os filtros e, se desejar, você pode marcar os filtros como parâmetros e exibir os resultados da consulta. Em seguida, salve as alterações no servidor ou no site.  
  
     ![rs_SharedDatasetDesignMode](../media/rs-shareddatasetdesignmode.gif "rs_SharedDatasetDesignMode")  
  
 Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados &#40;Construtor de Relatórios e SSRS&#41;](embedded-and-shared-datasets-report-builder-and-ssrs.md) e [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md).  
  
 Você também pode adicionar conjuntos de dados a um relatório adicionando partes de relatório que incluem os conjuntos de dados dos quais elas dependem. [!INCLUDE[ssRBrptparts](../../../includes/ssrbrptparts-md.md)]  
  
 Para saber como criar um relatório que exibe dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Tutorial: Criando um relatório de tabela básico &#40;Construtor de Relatórios&#41;](../tutorial-creating-a-basic-table-report-report-builder.md). Para criar um relatório que inclui seus próprios dados, consulte [Tutorial: Criar um gráfico de relatório rápido offline &#40;Construtor de Relatórios&#41;](../report-builder/tutorial-create-a-quick-chart-report-offline-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Methods"></a>Adicionando dados de relatório  
 No Construtor de Relatórios, você pode adicionar dados de relatório das seguintes maneiras.  
  
-   Adicione partes de relatório de um servidor de relatório ao seu relatório. Cada parte de relatório é autossuficiente e inclui conjuntos de dados dependentes. Os conjuntos de dados são predefinidos.  
  
-   Use os assistentes de Tabela/Matriz, Gráfico e Mapa. Com os assistentes, é possível selecionar fontes de dados compartilhadas e conjuntos de dados compartilhados, ou criar novos conjuntos de dados, e continuar criando o relatório.  
  
-   Adicione conjuntos de dados compartilhados de um servidor de relatório. Os conjuntos de dados compartilhados são predefinidos e especificam quais dados devem ser usados de uma fonte de dados predefinida. Ao adicionar um conjunto de dados compartilhado ao relatório, você adiciona uma referência de conjunto de dados que aponta para a definição do conjunto de dados compartilhado.  
  
 No Construtor de Relatórios ou Designer de Relatórios, você pode adicionar dados das seguintes maneiras.  
  
-   Adicione conjuntos de dados inseridos com base nas fontes de dados compartilhadas.  
  
-   Adicione conjuntos de dados inseridos com base nas fontes de dados inseridas.  
  
> [!NOTE]  
>  Em um servidor de relatório, os itens compartilhados são protegidos individualmente ou herdando permissões da pasta onde eles são publicados. Para permitir que outros usuários acessem os conjuntos de dados compartilhados que você salva, é necessário entender como as permissões são concedidas. Para obter mais informações, consulte [Segurança &#40;Construtor de Relatórios&#41;](../report-builder/security-report-builder.md) ou [Proteger itens de conjuntos de dados compartilhados](../security/secure-shared-dataset-items.md).  
  
 Depois de adicionar dados a um relatório, você pode organizar os dados na página de relatório com regiões de dados, modificar partes de relatório e compartilhar essas alterações com outros, além de permitir que os usuários limitem ou classifiquem os dados no relatório. Para obter mais informações, consulte os seguintes tópicos relacionados:  
  
-   [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
-   [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)  
  
-   [Minigráficos e barras de dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
-   [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](../report-design/indicators-report-builder-and-ssrs.md)  
  
-   [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-parts-report-builder-and-ssrs.md)  
  
-   [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  

##  <a name="QuickStart"></a>Adicionando dados com partes de relatório  
 As partes de relatório contêm os conjuntos de dados dos quais elas dependem. Esses conjuntos de dados são criados em fontes de dados compartilhadas que estão disponíveis no servidor de relatório. No Construtor de Relatórios, quando você adiciona uma parte de relatório ao relatório, os conjuntos de dados dependentes são adicionados ao relatório, como se você os tivesse adicionado manualmente. Por exemplo, um gráfico predefinido contém um conjunto de dados. Para ver os dados, visualize o relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBrptparts](../../../includes/ssrbrptparts-md.md)]  
  
 Partes de relatório, fontes de dados compartilhadas e conjuntos de dados compartilhados são definidos antecipadamente e salvos em um servidor de relatório. Para acessá-los, você precisa abrir o Construtor de Relatórios no modo de servidor conectando-se ao servidor de relatório. Você pode usá-los para criar suas próprias versões se tiver permissões de gravação no servidor de relatório.  
  
-   Para obter mais informações, consulte [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-parts-report-builder-and-ssrs.md) e [Partes de relatório no Designer de Relatórios &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md).  

##  <a name="Queries"></a>Consultas e designers de consulta  
 Para especificar quais dados deseja em uma fonte de dados, crie um comando de consulta. Cada tipo de fonte de dados fornece um *designer de consulta* relacionado para ajudar você a criar a consulta. O designer de consulta pode ser gráfico ou baseado em texto. Em um designer de consulta gráfica, você exibe metadados que representam os dados na fonte de dados externa e criam interativamente uma consulta arrastando campos ou entidades para a superfície de design de consulta. Em um designer de consulta baseado em texto, você escreve ou importa consultas na sintaxe de consulta que tem suporte da fonte de dados externa.  
  
 No designer de consulta, você pode executar a consulta para exibir dados de exemplo e validar a sintaxe do comando de consulta. Os nomes de coluna no conjunto de resultados tornam-se os nomes de campo que você vê no painel Dados do Relatório. O conjunto de resultados deve ser um único conjunto de linhas e colunas em que o mesmo número de valores existe para cada linha de dados. Não há suporte para vários conjuntos de resultados a partir de uma única consulta. Não há suporte para hierarquias imperfeitas, que não têm um número constante de colunas e podem gerar um número diferente de valores de dados para cada linha.  
  
 Para executar uma consulta, é necessário ter credenciais de tempo de design. Para obter mais informações, consulte [especificar credenciais em Construtor de relatórios](../specify-credentials-in-report-builder.md) e [conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 A comunicação entre uma extensão de dados e a fonte de dados externa é gerenciada pelos provedores de dados. O suporte para sintaxe do comando de consulta, parâmetros de consulta e tipos de dados para obter valores no conjunto de resultados é determinado por cada provedor de dados. Para obter mais informações, consulte o tópico para o tipo específico de extensão de dados e [Designers de Consulta &#40;Construtor de Relatórios&#41;](../query-designers-report-builder.md).  

##  <a name="HowTo"></a> Tópicos de instruções  
 [Adicionar e verificar uma conexão de dados ou uma fonte de dados &#40;Construtor de Relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Criar um conjunto de um DataSet compartilhado ou um conjunto de &#40;inserido Construtor de Relatórios e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Adicione, edite, atualize campos no painel de dados do relatório &#40;Construtor de Relatórios e SSRS&#41;](add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md)  
  
 [Crie uma consulta no designer de consulta relacional &#40;Construtor de Relatórios e SSRS&#41;](build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)  
  
 [Mostrar conjuntos de dados ocultos para obter os valores de parâmetro para &#40;s multidimensionais Construtor de Relatórios e SSRS&#41;](show-hidden-datasets-for-parameter-values-multidimensional-data.md)  
  
 [Adicionar um filtro a um conjunto de &#40;Construtor de Relatórios e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
 [Definir uma mensagem sem dados para uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](set-a-no-data-message-for-a-data-region-report-builder-and-ssrs.md)  
  
 [Associar um parâmetro de consulta a um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md)  
  
 [Definir parâmetros no designer de consulta MDX para Analysis Services &#40;Construtor de Relatórios e SSRS&#41;](define-parameters-in-the-mdx-query-designer-for-analysis-services.md)  

##  <a name="Section"></a> Nesta seção  
 [Partes de relatório e conjuntos de dados no Construtor de Relatórios](report-parts-and-datasets-in-report-builder.md)  
  
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
 [Especificar as credenciais no Construtor de Relatórios](../specify-credentials-in-report-builder.md)  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  

## <a name="see-also"></a>Consulte Também  
 [Modo de exibição de Design de relatório &#40;Construtor de Relatórios&#41;](../report-builder/report-design-view-report-builder.md)   
 [Conceitos de criação de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
