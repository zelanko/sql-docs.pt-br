---
title: Dados do Relatório
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: be36e61a44a416283e77638f01005f1b3e16883b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67413055"
---
# <a name="report-data-in-sql-server-reporting-services-ssrs"></a>Relatório de Dados no SSRS (SQL Server Reporting Services)

  Os dados do relatório podem vir de várias fontes de dados de sua organização. Sua primeira etapa de criação de um relatório é criar fontes de dados e conjuntos de dados que representem os dados de relatório subjacentes. Cada fonte de dados inclui informações sobre a conexão de dados. Cada conjunto de dados inclui um comando de consulta que define o conjunto de campos a serem usados como dados de uma fonte de dados. Para visualizar os dados de cada conjunto de dados, adicione uma região de dados, como uma tabela, uma matriz ou um mapa. Quando o relatório é processado, as consultas são executadas na fonte de dados e cada região de dados é expandida conforme necessário para exibir os resultados da consulta do conjunto de dados.  
  
##  <a name="BkMk_ReportDataTerms"></a> Termos

 Se você não estiver familiarizado com [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] os conceitos, examine os termos a seguir em [Reporting Services conceitos &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md): *conexão de dados*, *fontes de dados inseridas*, *fontes de dados compartilhadas*, *DataSets inseridos*, DataSets *compartilhados*, *consultas de DataSet*, *partes de relatório*e *alertas de dados*.  
  
##  <a name="BkMk_ReportDataTips"></a>Dicas para especificar dados de relatório

 Use as informações a seguir para criar sua estratégia de dados de relatório.  
  
- **Fontes de dados** As fontes de dados podem ser publicadas e gerenciadas independentemente dos relatórios em um servidor de relatório ou site do SharePoint. Para cada fonte de dados, você ou o proprietário do banco de dados pode gerenciar as informações de conexão em um local. As credenciais de fonte de dados são armazenadas com segurança no servidor de relatório; você não inclui senhas na cadeia de conexão. Você pode redirecionar uma fonte de dados de um servidor de teste para um servidor de produção. Você pode desabilitar uma fonte de dados para suspender todos os relatórios que a usam. Para obter uma lista de fontes de dados com suporte, consulte [conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
- **Conjuntos** de os Os conjuntos de dados podem ser publicados e gerenciados de forma independente dos relatórios ou das fontes de dados compartilhadas das quais dependem. Você ou o proprietário do banco de dados pode fornecer consultas otimizadas para uso por autores de relatório. Quando você altera a consulta, todos os relatórios que usam o de conjunto de dados compartilhado usam a consulta atualizada. Você pode habilitar o cache de conjunto de dados para melhorar o desempenho. Você pode agendar cache de consulta par um momento específico ou usar uma agenda compartilhada.  
  
- **Dados usados por partes de relatório** As partes de relatório podem incluir os dados dos quais dependem. Para obter mais informações sobre partes de relatório, consulte [Partes de relatório no Designer de Relatórios &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md).  
  
- **Filtrar dados** Os dados do relatório podem ser filtrados na consulta ou no relatório. Você pode usar conjuntos de dados e variáveis de consulta para criar parâmetros em cascata e fornecer aos usuários a capacidade de refinar escolhas de milhares de seleções para um número mais fácil de gerenciar. Você pode filtrar dados em uma tabela ou gráfico com base em valores de parâmetros ou outros valores que você especifica.  
  
- **Parâmetros** do Os comandos de consulta do conjunto de relatórios que incluem variáveis de consulta criam automaticamente parâmetros de relatório correspondentes. Também é possível criar parâmetros manualmente. Quando você exibe um relatório, a barra de ferramentas de relatório exibe os parâmetros. Os usuários podem selecionar valores para controlar os dados ou a aparência do relatório. Para personalizar dados de relatório para audiências específicas, você pode criar conjuntos de parâmetros de relatório com diferentes valores padrão vinculados à mesma definição de relatório ou usar o campo interno `UserID`. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md) e [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
- **Alertas de dados** Depois que um relatório é publicado, você pode criar alertas com base em dados de relatório e receber mensagens de email quando ele atender às regras que você especificar.  
  
- **Agrupar e agregar dados** Os dados do relatório podem ser agrupados e agregados na consulta ou no relatório. Se você agregar valores na consulta, poderá continuar a combinar valores no relatório dentro das restrições do que é significativo.  Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md) e [Função de agregação &#40;Construtor de Relatórios e SSRS&#41;](../report-design/report-builder-functions-aggregate-function.md).  
  
- **Classificar dados** Os dados do relatório podem ser classificados na consulta ou no relatório. Em tabelas, você também pode adicionar um botão de classificação interativo para permitir que o usuário controle a ordem de classificação.  
  
- **Dados baseados em expressão** Como a maioria das propriedades de relatório pode ser baseada em expressão, e as expressões podem incluir referências a campos de conjunto de dados e parâmetros de relatório, você pode escrever expressões poderosas para controlar os dados e a aparência do relatório. Você pode fornecer a um usuário a capacidade de controlar os dados que eles vê por meio da definição de parâmetros.  
  
- **Exibir dados de um DataSet** Normalmente, os dados de um DataSet são exibidos em uma ou mais regiões de dados, por exemplo, uma tabela e um gráfico.  
  
- **Exibir dados de vários conjuntos de** dados  Você pode escrever expressões em uma região de dados com base em um conjunto que procure valores ou agregações em outros conjuntos de dados. Você pode incluir sub-relatórios em uma tabela com base em um conjunto de dados para exibir os dados de outra fonte de dados.  
  
## <a name="data-connections-data-sources-and-datasets"></a>Conexões de dados, fontes de dados e conjuntos de dados

 Use a lista a seguir para ajudar a definir fontes de dados para um relatório.  
  
- Considere se fontes de dados e conjuntos de dados inseridos ou compartilhados devem ser usados. Colabore com os proprietários de fontes de dados para implementar e usar tecnologia de autenticação e autorização adequada para sua organização.  
  
- Compreenda a arquitetura da camada de dados do software de sua organização e os problemas potenciais oriundos dos tipos de dados. Compreenda como as extensões de dados e as extensões de processamento de dados podem afetar os resultados da consulta. Os tipos de dados diferem entre a fonte de dados, os provedores de dados e os tipos de dados armazenados no arquivo de definição de relatório (.rdl).  
  
- Compreenda as arquiteturas e as ferramentas de cliente/servidor do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Por exemplo, no Designer de Relatórios, você cria relatórios em uma máquina cliente que usa tipos de fonte de dados internos. Quando você publica um relatório, os tipos de fonte de dados devem ter suporte no servidor de relatório ou no site do SharePoint.  Para obter mais informações, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
- As fontes de dados e os conjuntos de dados são criados em um relatório e publicados em um servidor de relatório ou site do SharePoint em uma ferramenta de criação de cliente. As fontes de dados podem ser criadas diretamente no servidor de relatório. Depois de elas serem publicadas, você pode configurar credenciais e outras propriedades no servidor de relatório. Para obter mais informações, consulte [Data Connections, Data Sources, and Connection Strings in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) and [Reporting Services Tools](../tools/reporting-services-tools.md).  
  
- As fontes de dados que você pode usar dependem de quais extensões de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] estão instaladas. O suporte para fontes de dados pode diferir por ferramenta de criação de cliente, por versão do servidor de relatório e por plataforma de servidor de relatório. Para obter mais informações, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
- As credenciais de fonte de dados variam de acordo com o tipo de fonte de dados e de se você está exibindo relatórios em seu cliente ou servidor de relatório ou site do SharePoint. Para obter mais informações, consulte [Definir permissões para itens do Servidor de Relatório em um site do SharePoint &#40;Reporting Services no modo integrado do SharePoint&#41;](../security/set-permissions-for-report-server-items-on-a-sharepoint-site.md), [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../integration-services/connection-manager/data-sources.md) e informações de credenciais específicas a cada ferramenta em [Ferramentas do Reporting Services](../tools/reporting-services-tools.md).  
  
## <a name="related-tasks"></a>Related Tasks

 A tarefas relacionadas à criação de conexões de dados, à adição de dados de origens externas, conjuntos de dados e consultas.  
  
|||  
|-|-|  
|**Tarefas comuns**|**Links**|  
|Criar conexões de dados|[Data Connections, Data Sources, and Connection Strings in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|Criar conjuntos de dados e consultas|[Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|  
|Gerenciar fontes de dados depois de elas serem publicadas|[Gerenciar fontes de dados de relatório](manage-report-data-sources.md)|  
|Gerenciar conjuntos de dados compartilhados depois de eles serem publicados|[Gerenciar conjuntos de dados compartilhados](manage-shared-datasets.md)|  
|Criar e gerenciar alertas de dados|[Reporting Services Data Alerts](../tutorial-creating-a-basic-table-report-report-builder.md)|  
|Armazenar um conjunto de dados compartilhado|[Conjuntos de dados compartilhados em cache &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)|  
|Agendar um conjunto de dados compartilhado para pré-carregar o cache|[Agendas](../subscriptions/schedules.md)|  
|Adicionar uma extensão de dados|[Implementando uma extensão de processamento de dados](../extensions/data-processing/implementing-a-data-processing-extension.md)|