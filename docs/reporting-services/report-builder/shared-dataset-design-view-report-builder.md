---
title: Modo de exibição de Design do conjunto de dados compartilhado (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 47c502da-d163-45d9-bf04-0849e5ba7929
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4b00e626bf9823d45d7437bfa3219fb2b0afa8cc
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287937"
---
# <a name="shared-dataset-design-view-report-builder"></a>Exibição do design de conjunto de dados compartilhados (Construtor de Relatórios)
  Em um relatório, um conjunto de dados representa dados de relatório retornados em virtude da execução de um consulta em uma fonte de dados externa. Conjuntos de dados compartilhados são publicados em um servidor de relatório e podem ser usados por vários relatórios. Você pode criar conjuntos de dados para compartilhar com outras pessoas. Na janela Design de Conjunto de Dados Compartilhado, você pode selecionar uma fonte de dados compartilhada, especificar as propriedades do conjunto de dados compartilhado e criar uma consulta no designer de consultas.  
  
 ![rs_SharedDatasetDesignMode](../../reporting-services/report-builder/media/rs-shareddatasetdesignmode.gif "rs_SharedDatasetDesignMode")  
  
 Para obter mais informações sobre como trabalhar com dados em um relatório, consulte [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md).  
  
##  <a name="Ribbon"></a> A Faixa de Opções  
 A Faixa de Opções o ajuda a localizar os comandos de que você precisa para executar uma tarefa. Os comandos são organizados nos seguintes grupos lógicos: Conexão, Conjunto de dados e Designer de consultas.  
  
### <a name="connection"></a>Conexão  
 Use o botão **Selecionar** no grupo Conexão para selecionar uma fonte de dados compartilhada no relatório ou navegar até uma fonte de dados compartilhada no servidor de relatório.  
  
> [!NOTE]  
>  Um conjunto de dados compartilhado deve ser baseado em uma fonte de dados compartilhada. Se a fonte de dados de que você precisa não estiver disponível, será necessário criar uma no servidor de relatório. Para obter mais informações, consulte [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
 Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão](https://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
### <a name="dataset"></a>Dataset  
 Use o botão **Definir Opções** para definir propriedades de conjunto de dados compartilhadas. Entre elas estão as seguintes:  
  
-   Campos. Você pode adicionar ou editar um campo na coleção de campos.  
  
-   Opções de dados. Você pode definir opções que afetam os critérios de correspondência e a ordem de classificação, como diferenciar maiúsculas de minúsculas e ordenação.  
  
-   Filtros. Você pode definir filtros que limitam os dados em um relatório depois que eles são recuperados da conexão de dados.  
  
-   Parâmetros. Você pode adicionar um parâmetro ou editar opções de parâmetro. Por exemplo, é possível especificar um valor padrão para cada parâmetro de forma que você possa criar um plano de atualização de cache para esse conjunto de dados compartilhado no servidor de relatório.  
  
 Os valores que você define tornam-se parte da definição do conjunto de dados compartilhado no servidor de relatório. Quando um autor de relatório inclui o conjunto de dados compartilhado em um relatório, as opções que você especifica se aplicam a essa instância de conjunto de dados.  
  
 Depois que um conjunto de dados compartilhado é adicionado a um relatório, o autor do relatório pode substituir as seguintes opções: ordenação, diferenciação de maiúsculas e minúsculas, diferenciação de acentuação, diferenciação de kanatype, diferenciação de largura, subtotais. Eles também podem criar filtros de conjunto de dados adicionais para limitar os dados no relatório.  
  
 Para obter mais informações, consulte [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).  
  
 Para obter mais informações sobre planos de atualização de cache, consulte [Armazenar conjuntos de dados compartilhados em cache &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md).  
  
### <a name="query-designer"></a>Designer de Consulta  
 Use a barra de ferramentas do designer de consulta para ajudar criar uma consulta que especifique quais dados serão recuperados da conexão de dados. A barra de ferramentas exibida depende do designer de consulta associado ao tipo de fonte de dados na conexão de dados.  
  
 Para obter mais informações, consulte o tópico que corresponde ao tipo de fonte de dados em [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md).  
  
  
##  <a name="DesignSurface"></a> A Superfície do Designer de Consulta  
 Um designer de consulta o ajuda a criar uma consulta na sintaxe exigida pela fonte de dados externa.  
  
 Alguns tipos de fontes de dados fornecem um designer de consultas gráficas que você pode usar para explorar os metadados em uma fonte de dados externa. Você pode arrastar nomes interativamente do painel de metadados para a superfície do design de consulta ou interativamente seleciona os nomes a serem usados.  
  
 Alguns tipos de fonte de dados dão suporte a um designer de consultas baseadas em texto que você pode usar para colar nas consultas que você criou em outras ferramentas, como o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Cada tipo de fonte de dados possui requisitos específicos para a consulta que funcionará na fonte de dados externa. Para obter mais informações, consulte o tópico que corresponde ao tipo de fonte de dados em [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) e [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
  
##  <a name="Results"></a> Exibindo resultados de consultas  
 No modo de design do conjunto de dados compartilhado, você está criando uma consulta que recupera dados da conexão de dados quando o relatório é processado.  
  
 Execute a consulta para consultar dados de exemplo da conexão de dados e verificar se a consulta retorna o tipo de dados que você espera. As colunas no conjunto de resultados provêm dos metadados para esquemas de dados da conexão de dados. Os nomes de coluna tornam-se a coleção de campos de conjunto de dados. Os valores dos dados exibidos no conjunto de resultados da consulta são dados de tempo de design. Depois que você salva o conjunto de dados compartilhado como uma definição de conjunto de dados compartilhado no servidor de relatório, apenas o texto da consulta é salvo. Os dados no conjunto de resultados da consulta não são salvos.  
  
 Quando um autor de relatório adiciona esse conjunto de dados compartilhado a um relatório, um ponteiro para a definição de conjunto de dados no servidor de relatório é adicionado. No relatório, a coleção de campos de conjunto de dados é exibida no painel de dados do relatório. O texto da consulta não está disponível.  
  
 As credenciais que você usa para executar uma consulta são independentes das credenciais usadas para visualizar um relatório ou executar um relatório do servidor de relatório. Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
### <a name="running-a-report-with-parameters"></a>Executando um relatório com parâmetros  
 Quando uma consulta inclui variáveis de consulta, os parâmetros de conjunto de dados são criados automaticamente. Por sua vez, quando você conclui a criação da consulta de conjunto de dados, os parâmetros da consulta definidos como parâmetros de conjunto de dados são criados automaticamente.  
  
 Se um relatório contiver parâmetros, todos os parâmetros deverão ter valores padrão para que o relatório possa ser executado automaticamente. Se um parâmetro não tiver um valor padrão, quando o relatório for executado, você deverá escolher um valor para o parâmetro e clicar em **Exibir Relatório** na guia **Executar** .  
  
 Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Save"></a> Salvando o conjunto de dados compartilhado  
 Para salvar a consulta que você criou, no botão **Construtor de Relatórios** , clique em **Salvar** ou em **Salvar como**. Navegue até a pasta apropriada no servidor de relatório e salve a definição de conjunto de dados compartilhada. O conjunto de dados compartilhado não estará disponível para os outros até que você o salve no servidor de relatório.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  
