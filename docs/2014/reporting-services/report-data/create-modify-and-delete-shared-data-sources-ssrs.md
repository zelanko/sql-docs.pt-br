---
title: Criar, modificar e excluir fontes de dados compartilhadas (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- modifying data source properties
- shared data sources [Reporting Services]
- removing shared data sources
- roles [Reporting Services], shared data sources
- data sources [Reporting Services], shared
- data sources [Reporting Services], modifying properties
- deleting shared data sources
ms.assetid: 1e58c1c2-5ecf-4ce6-9d04-0a8acfba17be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4a2239e07cc24842c5cbdf44c8743ea2d79ea7cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107397"
---
# <a name="create-modify-and-delete-shared-data-sources-ssrs"></a>Criar, modificar e excluir fontes de dados compartilhadas (SSRS)
  Uma fonte de dados compartilhada é um conjunto de propriedades de conexão de fonte de dados que pode ser referenciada por vários relatórios, modelos e assinaturas controladas por dados que são executados em um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . As fontes de dados compartilhadas fornecem um modo fácil de gerenciar as propriedades da fonte de dados que geralmente são alteradas com o passar do tempo. Se a conta de usuário ou senha for alterada ou se você mover o banco de dados para outro servidor, as informações de conexão poderão ser atualizadas em um único lugar.  
  
 As fontes de dados compartilhadas são opcionais para relatórios e assinaturas controladas por dados, mas são obrigatórias para modelos de relatórios. Se você planeja usar os modelos de relatório para relatórios ad hoc, deve criar e manter um item fonte de dados compartilhada para fornecer informações de conexão ao modelo.  
  
 Uma fonte de dados compartilhada é composta pelas seguintes partes:  
  
|Parte|Descrição|  
|----------|-----------------|  
|Nome|Um nome que identifica o item dentro da hierarquia de pastas do servidor de relatórios.|  
|Descrição|Uma descrição que aparece com o item no Gerenciador de Relatórios quando você exibe os conteúdos da pasta.|  
|Tipo de conexão|A extensão de processamento de dados usada com a fonte de dados. Você só poderá usar extensões de processamento de dados que estiverem implantadas no servidor de relatórios. Para obter mais informações sobre as extensões de processamento de dados incluídas no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md).|  
|Cadeia de conexão|A cadeia de conexão para o banco de dados. Para obter mais informações e exibir exemplos de cadeias de caracteres de conexão para fontes de dados usados com frequência, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).|  
|Tipo de credencial|Especifica como as credenciais são obtidas para a conexão e se elas serão usadas depois que a conexão for estabelecida. Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](../../integration-services/connection-manager/data-sources.md).|  
  
 Uma fonte de dados compartilhada não contém informações de consulta usadas para a recuperação de dados. A consulta sempre é mantida dentro de uma definição do relatório.  
  
## <a name="creating-and-modifying-a-shared-data-source"></a>Criando e modificando uma fonte de dados compartilhada  
 Para criar uma fonte de dados compartilhada ou modificar suas propriedades, é preciso ter permissões para **Gerenciar fontes de dados** no servidor de relatório. Se o servidor de relatórios for executado em modo nativo, você poderá usar o Gerenciador de Relatórios para criar e configurar a fonte de dados compartilhada. Se o servidor de relatórios for executado no modo integrado do SharePoint, use as páginas de aplicativo em um site do SharePoint. Para qualquer servidor de relatórios independentemente de seu modo, você pode criar uma fonte de dados compartilhada no Designer de Relatórios e publicá-la em um servidor de destino.  
  
 Para obter mais informações sobre como criar uma fonte de dados compartilhada, consulte:  
  
-   [Criar uma fonte de dados inserida ou compartilhada &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)  
  
-   [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)  
  
 Depois de criar uma fonte de dados compartilhada no servidor de relatórios, você poderá criar atribuições de função para controlar o acesso a ela, movê-la para outro local, renomeá-la ou torná-la offline para evitar o processamento de relatórios durante as operações de manutenção na fonte de dados externa. Se renomear ou mover um item fonte de dados compartilhada para outro local na hierarquia de pastas do servidor de relatórios, as informações de caminho em todos os relatórios ou assinaturas que fazem referência à fonte de dados compartilhada serão atualizadas. Ao colocar a fonte de dados no estado offline, todos os relatórios, modelos e assinaturas não serão executados enquanto a fonte de dados não for reativada.  
  
 Para obter mais informações sobre como controlar o acesso às fontes de dados compartilhadas na hierarquia de pastas do servidor de relatório, consulte [Proteger itens de fontes de dados compartilhadas](../security/secure-shared-data-source-items.md).  
  
## <a name="deleting-a-shared-data-source"></a>Excluindo uma fonte de dados compartilhada  
 Você pode excluir uma fonte de dados compartilhada da mesma forma que exclui qualquer item do servidor de relatórios. No Gerenciador de relatórios, você abra a pasta na exibição de detalhes, selecione o item e clique em **excluir**. Na página do aplicativo em um site do SharePoint, abra a biblioteca do SharePoint, selecione o item e clique em **excluir**.  
  
 A exclusão de uma fonte de dados compartilhada desabilitará todos os relatórios, modelos ou assinaturas controladas por dados que a usam. Sem as informações de conexão da fonte de dados, os itens não poderão ser executados. Para habilitar esses itens, abra cada um deles e siga as etapas a seguir:  
  
-   Para os relatórios e as assinaturas controlados por dados que fazem referência à fonte de dados compartilhada, você pode especificar as informações de conexão da fonte de dados nas propriedades do relatório ou da assinatura, ou também pode selecionar uma nova fonte de dados compartilhada que contenha os valores desejados.  
  
-   Para modelos e relatórios do Construtor de Relatórios que usam esse modelo, é preciso especificar uma nova fonte de dados compartilhada. Os modelos podem obter as informações de conexão da fonte de dados somente pelas fontes de dados compartilhadas.  
  
 Para exibir a lista de relatórios e modelos que usam a fonte de dados, abra a página Itens Dependentes da fonte de dados compartilhada. Você pode acessar essa página quando abrir a fonte de dados no Gerenciador de Relatórios ou uma página de aplicativo do SharePoint. Observe que a página Itens Dependente não mostra as assinaturas controladas por dados. Se uma fonte de dados compartilhada for usada por uma assinatura, a assinatura não será exibida na lista de itens dependentes.  
  
 Não existe a operação Desfazer para a exclusão de uma fonte de dados compartilhada. Entretanto, em caso de exclusão acidental, você poderá criar uma nova fonte de dados compartilhada usando os mesmos valores de propriedades daquela que foi excluída. Também será preciso abrir cada relatório, modelo e assinatura controlada por dados para reassociar a fonte de dados compartilhada ao item que a usa, mas como as propriedades serão as mesmas, os relatórios, os modelos e as assinaturas continuarão funcionando normalmente.  
  
## <a name="see-also"></a>Consulte também  
 [Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)   
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Gerenciar fontes de dados de relatório](manage-report-data-sources.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Página de propriedades Fontes de Dados &#40;Gerenciador de Relatórios&#41;](../data-sources-properties-page-report-manager.md)   
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Configurar propriedades de fonte de dados para um relatório &#40;Gerenciador de Relatórios&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
