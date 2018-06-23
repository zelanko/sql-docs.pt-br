---
title: Gerenciar fontes de dados de relatório | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- reports [Reporting Services], data
- published reports [Reporting Services], data source connections
- shared data sources [Reporting Services]
- data sources [Reporting Services], managing
ms.assetid: 0475aded-c8fe-4337-a2b5-4df0ec4c46af
caps.latest.revision: 51
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 8be62bb127d6d3fed0f3156f1dc58fc276e51431
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007230"
---
# <a name="manage-report-data-sources"></a>Gerenciar fontes de dados de relatório
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], relatórios, modelos de relatório e assinatura controladas por dados recuperam dados de fontes de dados externas. Para se conectar a uma fonte de dados externo, um servidor de relatório usa as informações de conexão de fonte de dados definidas em ou às quais é feita referência no relatório, modelo ou assinatura. As propriedades de conexão da fonte de dados são sempre definidas na criação do relatório ou modelo, mas podem ser gerenciadas de forma independente depois que o relatório ou modelo é publicado em um servidor de relatório.  
  
 Para gerenciar fontes de dados de relatório, você pode usar o Gerenciador de Relatórios para um servidor de relatório no modo nativo ou páginas do aplicativo em um site do SharePoint, caso você tenha implantado o servidor de relatório no modo integrado do SharePoint.  
  
 O gerenciamento de conexões de fonte de dados é caracterizado pelas seguintes tarefas, que são descritas neste tópico:  
  
-   Alterar cadeias de conexão.  
  
-   Alterar credenciais.  
  
-   Criar e usar fontes de dados compartilhadas em um servidor de relatório, incluindo alternância de uma fonte de dados inserida para uma fonte de dados compartilhada.  
  
-   Controlar acesso a propriedades de fonte de dados definindo permissões em um relatório, modelo ou em qualquer fonte de dados compartilhada em uso.  
  
 Observe que a modificação de consultas não faz parte do gerenciamento de conexão da fonte de dados. Para modificar uma consulta em um relatório ou modelo, você deve usar uma ferramenta de autoria e fazer suas alterações na definição do relatório ou do modelo.  
  
## <a name="managed-properties-data-source-type-connection-strings-and-credentials"></a>Propriedades gerenciadas: tipo de fonte de dados, cadeias de conexão e credenciais  
 As propriedades da fonte de dados que você pode gerenciar em um servidor de relatório são:  
  
|Propriedade|Description|Como gerenciá-la|  
|--------------|-----------------|----------------------|  
|Tipo de fonte de dados|Determina qual extensão de processamento de dados do servidor de relatório será usada nos dados externos. Alguns exemplos de processadores de dados incluem SQL Server, Analysis Services e Oracle.|O tipo de fonte de dados é uma propriedade gerenciada, pois é configurável. Entretanto, você deverá configurar apenas um tipo de fonte de dados se estiver criando uma nova fonte de dados compartilhada.<br /><br /> Não altere o tipo da fonte de dados nas páginas de propriedades de um relatório publicado ou modelo, pois isso certamente invalidará a conexão. É improvável que as estruturas de dados requeridas por um relatório ou modelo sejam idênticas em uma plataforma de dados diferente.|  
|Cadeia de conexão|Estabelece a conexão inicial a uma fonte de dados externa. Um relatório pode usar cadeias de conexões estáticas ou dinâmicas.<br /><br /> Uma *cadeia de conexão estática* é um conjunto de valores que o relatório usa para conectar-se à mesma fonte de dados sempre que é executado.<br /><br /> Uma *cadeia de conexão dinâmica* é uma expressão que você cria em um relatório, permitindo que o usuário selecione qual fonte de dados deve ser usada no tempo de execução. Você deve criar uma expressão e uma lista de seleção de fonte de dados no relatório ao criá-lo no Designer de Relatórios.|A alteração de uma cadeia de conexão é útil quando você move uma fonte de dados para outro computador, ou se você tiver criado relatórios usando dados de teste mas deseja implantar os relatórios com um banco de dados de produção.<br /><br /> Você pode gerenciar uma cadeia de conexão estática substituindo a cadeia original por uma diferente.<br /><br /> Para gerenciar uma cadeia de conexão dinâmica no Gerenciador de Relatórios ou em um site do SharePoint, você está limitado a substituí-la por uma estática. Não é possível editar a própria expressão, nem alterar a lista de seleção de fonte de dados. Para alterar a expressão ou a lista de valores válidos, você deve editar a definição do relatório e republicá-lo no servidor de relatório. Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).|  
|Credenciais|Fornece o nome e a senha de um usuário que tem permissão para ler dados da fonte de dados.<br /><br /> Se a fonte de dados não aceitar autenticação (por exemplo, se a fonte de dados for um arquivo XML ou arquivo do sistema), você poderá configurar uma conta de execução autônoma para permitir que o servidor de relatório conecte-se a uma fonte de dados externa sem passar as credenciais.|Você pode gerenciar credenciais atualizando a conta do usuário ou uma senha, caso expire.<br /><br /> Você também pode alterar o modo de obtenção de credenciais (por exemplo, solicitando que os usuários insiram credenciais no tempo de execução).<br /><br /> Para que os usuários possam assinar um relatório, você deve configurar o relatório para usar credenciais armazenadas.|  
  
## <a name="creating-and-using-shared-data-sources"></a>Criando e usando fontes de dados compartilhadas  
 Se você publicar um relatório com propriedades de fonte de dados inseridas em um relatório, considere alternar para propriedades da fonte de dados compartilhada. Fontes de dados compartilhadas são mais fáceis de administrar, pois você pode atualizar credenciais e cadeias de conexões em uma página. Todos os relatórios, modelos e assinaturas controladas por dados que usam aquela fonte de dados adquirem as alterações imediatamente. Você também pode colocar uma fonte de dados offline, pausando efetivamente o relatório ou a assinatura para evitar a execução durante a solução de problemas ou a investigação de qualquer problema que possa surgir.  
  
## <a name="controlling-access-data-source-properties"></a>Controlando acesso às propriedades de fonte de dados  
 Por padrão, qualquer um que tenha permissão para gerenciar relatórios pode definir qualquer propriedade em um relatório, incluindo propriedades que determinam o tipo da fonte de dados, cadeia de conexão, credenciais e se os relatórios obtêm informações e uma fonte de dados inserida ou compartilhada. Para obter mais informações sobre quais tarefas e permissões controlam o acesso a propriedades de fonte de dados em um servidor de relatório de modo nativo, consulte [proteger itens de fonte de dados compartilhada](../security/secure-shared-data-source-items.md) e [proteger relatórios e recursos](../security/secure-reports-and-resources.md).  
  
 As permissões para exibir e editar propriedades de itens em uma biblioteca do SharePoint são determinadas pelo administrador do site. Para obter mais informações sobre quais permissões controlam o acesso a propriedades de conexão de fonte de dados, consulte [List Permission Reference para itens do servidor de relatório e sites do SharePoint](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
## <a name="how-to-work-with-data-source-properties-on-a-report-server"></a>Como trabalhar com propriedades de fonte de dados em um servidor de relatório  
 Você pode usar uma variedade de ferramentas para criar e modificar propriedades de fonte de dados. A tabela a seguir resume as abordagens e ferramentas e fornece um link para informações adicionais.  
  
|Tarefa|Ferramenta|Link|  
|----------|----------|----------|  
|Exibir exemplos de cadeias de conexão.||[Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|Escolher uma abordagem para obter credenciais para conectar-se a uma fonte de dados.||[Especificar informações de credenciais e de conexão para fontes de dados de relatório](specify-credential-and-connection-information-for-report-data-sources.md)|  
|Adicionar propriedades de conexão de fonte de dados a um arquivo de definição de relatório (.rdl).|Designer de Relatórios|[Criar uma fonte de dados inserida ou compartilhada &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md)|  
|Adicionar e vincular a um arquivo de fonte de dados compartilhada (.rds) em um projeto de relatório.|Designer de Relatórios|[Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](create-modify-and-delete-shared-data-sources-ssrs.md)|  
|Crie uma lista predefinida de fontes de dados que os usuários possam selecionar em tempo de execução. Quando um usuário solicita um relatório, este fornece uma lista de fontes de dados. O usuário deve selecionar qual fonte de dados usar antes de executar o relatório. Para acrescentar uma lista de seleção de fonte de dados a um relatório, você usa uma expressão.<br /><br /> Isto é conhecido como uma conexão de fonte de dados dinâmica.|Designer de Relatórios|[Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)|  
|Criar um item de fonte de dados compartilhada em um servidor de relatório.|Gerenciador de Relatórios|[Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de relatórios&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)|  
|Armazenar credenciais como um pré-requisito para criar assinaturas ou instantâneos de relatório.|Gerenciador de Relatórios|[Armazenar credenciais em uma fonte de dados do Reporting Services](store-credentials-in-a-reporting-services-data-source.md)|  
|Editar propriedades de conexão da fonte de dados em um relatório publicado.|Gerenciador de Relatórios|[Configurar propriedades de fonte de dados para um relatório &#40;Gerenciador de relatórios&#41;](configure-data-source-properties-for-a-report-report-manager.md)|  
|Criar um item de fonte de dados compartilhada em um servidor de relatório.|Site do SharePoint|[Criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md)|  
|Usar informações de conexão .odc existentes com um relatório.|Site do SharePoint|[Usar uma Conexão de dados do Office &#40;. odc&#41; com relatórios &#40;Reporting Services no SharePoint modo integrado&#41;](use-an-office-data-connection-odc-with-reports.md)|  
  
> [!NOTE]  
>  Gerenciar as conexões de fonte de dados para relatar fontes de dados não é o mesmo que gerenciar a conexão do servidor de relatório para o banco de dados do servidor de relatório. Para obter mais informações sobre uma conexão do servidor de relatório com seu armazenamento de dados interno, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;Gerenciador de Configurações do SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
## <a name="see-also"></a>Consulte também  
 [Associar um relatório ou modelo a uma fonte de dados compartilhados &#40;SSRS&#41;](bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de relatórios&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Armazenar as credenciais em uma fonte de dados do Reporting Services](store-credentials-in-a-reporting-services-data-source.md)   
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Fontes de dados suportadas pelo Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Gerenciamento de conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)  
  
  