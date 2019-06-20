---
title: Gerenciar conjuntos de dados compartilhados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 2cbb1fa3-959e-4df6-9887-ebc93cc1b686
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c498917b7f4f293d1721d09e68d1ba40672c1dc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107206"
---
# <a name="manage-shared-datasets"></a>Gerenciar conjuntos de dados compartilhados
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], os conjuntos de dados compartilhados recuperam dados de fontes de dados compartilhadas que se conectam a fontes de dados externas. Um conjunto de dados compartilhado fornece uma maneira de compartilhar uma consulta para ajudar a fornecer um conjunto de dados consistente para vários relatórios. A consulta do conjunto de dados pode incluir parâmetros de conjunto de dados. Você pode configurar um conjunto de dados compartilhado para armazenar em cache os resultados da consulta para combinações de parâmetros específicas no primeiro uso ou especificando uma agenda. Você pode usar um cache de conjunto de dados compartilhado em combinação com um cache de relatório e feeds de dados de relatório para ajudar a gerenciar o acesso a uma fonte de dados.  
  
 Os conjuntos de dados compartilhados usam apenas fontes de dados compartilhadas, não fontes de dados inseridas. Um conjunto de dados compartilhado pode ser baseado em qualquer fonte de dados de uma extensão de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com suporte ou em um modelo de relatório.  
  
## <a name="creating-and-using-shared-datasets"></a>Criando e usando conjuntos de dados compartilhados  
 Para criar um conjunto de dados compartilhado, você deve usar um aplicativo que crie um arquivo de definição de conjunto de dados compartilhado (.rsd). Você pode usar um dos aplicativos a seguir para criar um conjunto de dados compartilhado:  
  
-   Construtor de Relatórios   Use o modo de design de conjunto de dados compartilhado e salve o conjunto de dados compartilhado em um servidor de relatório ou site do SharePoint.  
  
-   Designer de Relatórios do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Crie conjuntos de dados compartilhados sob a pasta Conjunto de Dados Compartilhado no Gerenciador de Soluções. Para publicar um conjunto de dados compartilhado, implante-o em um servidor de relatório ou site do SharePoint.  
  
-   Carregue um arquivo de definição de conjunto de dados compartilhado (.rsd). Você pode carregar um arquivo no servidor de relatório ou site do SharePoint. Em um site do SharePoint. Um arquivo carregado não é validado em relação ao esquema até que o conjunto de dados compartilhado seja armazenado em cache ou use em um relatório.  
  
 A definição de conjunto de dados compartilhado inclui uma consulta, parâmetros de conjunto de dados, inclusive valores padrão, opções de dados, como diferenciação de maiúsculas e minúsculas, e filtros de conjunto de dados. Os valores definidos na definição são usados sempre que o conjunto de dados compartilhado é incluído em um relatório.  
  
 Para usar um conjunto de dados compartilhado em um relatório, você abre um aplicativo, como o Construtor de Relatórios, navega até o servidor de relatório ou site do SharePoint e seleciona o conjunto de dados compartilhado. Isso adiciona uma instância do conjunto de dados compartilhado ao relatório. No relatório, você não pode exibir ou alterar a consulta ou a fonte de dados compartilhada do conjunto de dados compartilhado. Você pode especificar um conjunto adicional de valores de propriedade de conjunto de dados que se apliquem à instância no relatório. Por exemplo, você pode adicionar um filtro ou alterar opções de dados, como diferenciação de maiúsculas e minúsculas. Para obter mais informações, consulte [Conjuntos de dados inseridos de relatório e conjuntos de dados compartilhados &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md) na [documentação do Construtor de Relatórios](https://go.microsoft.com/fwlink/?LinkId=154494) em msdn.microsoft.com.  
  
## <a name="managing-shared-datasets"></a>Gerenciando conjuntos de dados compartilhados  
 Para gerenciar as propriedades de um conjunto de dados compartilhado publicado, você pode usar o Gerenciador de Relatórios para um servidor de relatório no modo nativo ou páginas do aplicativo em um site do SharePoint, caso você tenha implantado o servidor de relatório no modo integrado do SharePoint. As tarefas que você pode executar em um conjunto de dados compartilhado dependem de suas atribuições de função e do nível do site e permissões em nível de item, inclusive permissões na pasta se a herança de permissões estiver em vigor. A segurança em nível de item de conjuntos de dados compartilhados segue o mesmo modelo da segurança em nível de item de relatórios. Para obter mais informações, consulte [Proteger itens de conjunto de dados compartilhados](../security/secure-shared-dataset-items.md).  
  
 Você pode gerenciar as propriedades de item de conjunto de dados compartilhado, inclusive a fonte de dados compartilhada a ser usada, independentemente do relatório que usa o conjunto de dados compartilhado ou a fonte de dados compartilhada da qual ele depende. Para alterar a consulta ou outras propriedades de conjunto de dados que fazem parte da definição do conjunto de dados compartilhado, você deve editar a definição.  
  
### <a name="manage-shared-dataset-item-properties"></a>Gerenciar propriedades de item de conjunto de dados compartilhado  
 A tabela a seguir lista as propriedades de item que podem ser alteradas para um item de conjunto de dados compartilhado.  
  
|||  
|-|-|  
|Editar nome|Alterar o nome do conjunto de dados compartilhado. Todas as referências de itens dependentes continuarão funcionando.|  
|Editar Descrição|Alterar a descrição do conjunto de dados compartilhado.|  
|Editar o tempo limite de execução da consulta|Definir o tempo limite de execução da consulta em segundos. Zere (0) segundo significa nenhum tempo limite. Determina o número de segundos antes do tempo limite da consulta do conjunto de dados se esgotar. Para especificar nenhum valor de tempo limite, use 0. Para obter mais informações, consulte [Definindo valores de tempo limite para processamento de relatórios e conjuntos de dados compartilhados &#40;SSRS&#41;](../report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md).|  
|Exibir itens dependentes|Exibir os itens que usam esse conjunto de dados compartilhado: partes de relatório publicadas, fontes de dados compartilhadas e relatórios.|  
  
 As seguintes propriedades de conjunto de dados compartilhado são configuradas automaticamente:  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|HasDataSourceCredentials|Se a fonte de dados compartilhada associada tem credenciais salvas no servidor de relatório.|  
|HasUserProfileDependencies|Se o relatório tem uma referência à coleção global Usuário em sua consulta ou expressões de filtro.|  
  
## <a name="viewing-or-changing-the-shared-dataset-definition"></a>Exibindo ou alterando a definição do conjunto de dados compartilhado  
 As propriedades do conjunto de dados compartilhado, inclusive a consulta, os parâmetros do conjunto de dados, os valores padrão, os filtros de conjunto de dados e as opções de dados, como ordenação e diferenciação entre maiúsculas e minúsculas, são salvas na definição do conjunto de dados compartilhado. Se você tiver permissões suficientes, poderá exibir e alterar a definição.  
  
 Para exibir ou alterar a definição do conjunto de dados compartilhado, edite-o em um aplicativo, como o Construtor de Relatórios no modo de design do conjunto de dados compartilhado. Depois de fazer alterações, salve a definição do conjunto de dados compartilhado novamente no servidor ou site.  
  
 Outra maneira de exibir a definição de conjunto de dados compartilhado no XML é usar a sintaxe de acesso de URL no Gerenciador de Relatórios. Por exemplo, para exibir os valores padrão de cada parâmetro do conjunto de dados, você pode usar o seguinte comando de acesso de URL para exibir uma definição de conjunto de dados compartilhado denominado DataSet1 no servidor de relatório:  
  
```  
http://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition  
```  
  
## <a name="controlling-access-to-the-shared-dataset-definition"></a>Controlando o acesso à definição do conjunto de dados compartilhado  
 Por padrão, as tarefas a seguir se aplicam a operações em conjuntos de dados compartilhados.  
  
-   **Exibir Relatórios** Exibir itens do conjunto de dados compartilhados e propriedades de item.  
  
-   **Relatórios de Consumo** Ler definições de conjunto de dados compartilhado.  
  
-   **Gerenciar Relatórios** Criar e excluir conjuntos de dados compartilhados e editar propriedades de conjunto de dados compartilhado.  
  
-   **Definir segurança de itens** Exibir e modificar configurações de segurança para conjuntos de dados compartilhados.  
  
 Para obter mais informações sobre quais tarefas e permissões controlam o acesso às propriedades de fonte de dados em um servidor de relatório no modo nativo, consulte [Proteger itens de conjunto de dados compartilhados](../security/secure-shared-dataset-items.md).  
  
 As permissões para exibir e editar propriedades de itens em uma biblioteca do SharePoint são determinadas pelo administrador do site. Para obter mais informações, consulte [Referência à permissão de listas e sites do SharePoint para itens do Servidor de Relatório](../security/sharepoint-site-and-list-permission-reference-for-report-server-items.md).  
  
## <a name="how-to-work-with-shared-dataset-properties-on-a-report-server"></a>Como trabalhar com propriedades de conjuntos de dados compartilhados em um servidor de relatório  
 Você pode usar uma variedade de ferramentas para trabalhar com conjuntos de dados compartilhados. A tabela a seguir resume as abordagens e ferramentas e fornece um link para informações adicionais.  
  
|Tarefa|Ferramenta|Link|  
|----------|----------|----------|  
|Adicionar um conjunto de dados compartilhado ou alterar propriedades da definição de conjuntos de dados compartilhados.|Salvar no Construtor de Relatórios.<br /><br /> Implantar no Designer de Relatórios.<br /><br /> Carregar um arquivo .rsd no Gerenciador de Relatórios.|[Conjuntos de dados inseridos de relatório e conjuntos de dados compartilhados &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md) na [documentação do Construtor de Relatórios](https://go.microsoft.com/fwlink/?LinkId=154494) em msdn.microsoft.com<br /><br /> [Página Carregar Arquivo &#40;Gerenciador de Relatórios&#41;](../upload-file-page-report-manager.md)<br /><br /> Se você carregar um conjunto de dados compartilhado antes da fonte de dados compartilhada da qual ele depende ser publicada, deverá associar o conjunto de dados compartilhado manualmente à fonte de dados compartilhada. Para obter mais informações, veja [Página Propriedades Gerais, conjuntos de dados compartilhados &#40;Gerenciador de Relatórios&#41;](../general-properties-page-shared-datasets-report-manager.md).|  
|Alterar propriedades de item de conjunto de dados compartilhado.|Gerenciador de Relatórios|[Página Propriedades Gerais, conjuntos de dados compartilhados &#40;Gerenciador de Relatórios&#41;](../general-properties-page-shared-datasets-report-manager.md)|  
|Especificar propriedades adicionais de conjunto de dados compartilhado para uma instância de conjunto de dados compartilhado em um relatório.|Designer de Relatórios do Construtor de Relatórios|[Caixa de diálogo Propriedades do Conjunto de Dados, Consulta](../dataset-properties-dialog-box-query.md)|  
|Associar a uma fonte de dados compartilhada diferente para um conjunto de dados compartilhado.|Gerenciador de Relatórios|[Página Seleção de Fonte de Dados &#40;Gerenciador de Relatórios&#41;](../data-source-selection-page-report-manager.md)|  
|Verificar valores padrão para parâmetros de conjunto de dados.|Abrir no Construtor de Relatórios ou usar a sintaxe de acesso de URL.|Por exemplo:<br /><br /> `http://localhost/reportserver/?/DataSet1&rs:command=GetShareddatasetDefinition`|  
|Habilitar o cache|Gerenciador de Relatórios|[Conjuntos de dados compartilhados em cache &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)<br /><br /> [Página Cache, Conjuntos de Dados Compartilhados &#40;Gerenciador de Relatórios&#41;](../caching-page-shared-datasets-report-manager.md)|  
|Criar ou editar um plano de atualização de cache|Gerenciador de Relatórios|[Opções de atualização do cache &#40;Gerenciador de Relatórios&#41;](../cache-refresh-options-report-manager.md)|  
|Exibir o esquema de definição do conjunto de dados compartilhado.|Gerenciador de Relatórios|`http://<reportserver>/shareddatasetdefinition.xsd`|  
|No modo integrado do SharePoint, sincronizar a definição do conjunto de dados compartilhado entre o servidor de relatório e o site do SharePoint|Páginas do aplicativo do SharePoint|Alterar propriedades de item de conjunto de dados compartilhado<br /><br /> Alterar opções de cache<br /><br /> Alterar a fonte de dados compartilhada|  
  
## <a name="comparing-shared-datasets-with-other-report-server-items"></a>Comparando conjuntos de dados compartilhados com outros itens do servidor de relatório  
 Quando você gerencia vários tipos de itens em um servidor de relatório, ele ajuda a compreender como os itens são semelhantes e como são diferentes de outros itens do servidor de relatório.  
  
 Conjuntos de dados compartilhados são semelhantes a fontes de dados compartilhadas e a relatórios das seguintes maneiras:  
  
-   Como fontes de dados compartilhadas, os conjuntos de dados são gerenciados independentemente dos relatórios nos quais são usados. Parte do gerenciamento de um conjunto de dados compartilhado em um servidor de relatório é a capacidade de alterar a fonte de dados compartilhada da qual ele depende sem editar a definição do conjunto de dados compartilhado.  
  
-   Como relatórios, conjuntos de dados compartilhados podem ser armazenados em cache. As credenciais exigidas pela fonte de dados devem atender às restrições de armazenamento em cache, e os valores padrão devem ser especificados para cada parâmetro. Para obter mais informações, veja [Conjuntos de dados compartilhados em cache &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md).  
  
-   Como relatórios, a cada vez que o processamento ocorre, a definição atual do item no servidor de relatório é usada. Se você fizer alterações em um conjunto de dados compartilhado, cada relatório que o usa usará a definição atual no servidor de relatório quando o relatório for processado. Se o armazenando em cache estiver habilitado para o conjunto de dados compartilhado e você fizer alterações na definição do conjunto de dados compartilhado, as alterações não serão usadas até que os dados no cache expirem. Você pode usar planos de atualização de cache para ajudar a fornecer um conjunto e dados consistente para vários relatórios.  
  
 Conjuntos de dados são diferentes de partes de relatório publicadas da seguintes maneira:  
  
-   Ao contrário das partes de relatório publicadas, as alterações na definição do conjunto de dados compartilhado em um servidor de relatório não disparam notificações de atualização quando o relatório é aberto em um cliente de criação de relatório. Quando você executa o relatório, os dados da definição do conjunto de dados compartilhado no servidor de relatório são usados.  
  
 Conjuntos de dados compartilhados são semelhantes a assinaturas das seguintes maneiras:  
  
-   Conjuntos de dados compartilhados podem usar agendas específicas de item e compartilhadas para armazenamento em cache.  
  
-   Conjuntos de dados compartilhados seguem as mesmas regras para especificar valores de parâmetros que as assinaturas.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciamento do conteúdo do Servidor de Relatório &#40;Modo Nativo do SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [Concedendo permissões em um servidor de relatório no modo nativo](../security/granting-permissions-on-a-native-mode-report-server.md)  
  
  
