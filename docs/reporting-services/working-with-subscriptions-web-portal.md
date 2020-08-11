---
title: Trabalhando com assinaturas (portal da Web) | Microsoft Docs
description: Saiba como usar a página Assinaturas para listar todas as assinaturas do relatório atual no Reporting Services.
ms.date: 01/31/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 09e8ece5-0200-41f2-87c1-9fab19e261be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d5d936933b96c8d7f5c4c2830707b4a6bb4d9fe2
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243544"
---
# <a name="working-with-subscriptions-web-portal"></a>Trabalhando com assinaturas (portal da web)

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../includes/ssrs-appliesto-pbirs.md)]

Use a página Assinaturas para listar todas as assinaturas para o relatório atual. Se você tiver permissão adequada (como a contida na tarefa "Gerenciar todas as assinaturas"), você poderá exibir as assinaturas de todos os usuários. Caso contrário, essa página só mostrará as assinaturas que você possui.  
  
Antes de criar uma nova assinatura, você deve verificar se a fonte de dados do relatório armazena credenciais. Use a página de propriedades da Fonte de Dados para armazenar credenciais.  
  
> [!NOTE]
> O serviço SQL Server Agent precisa ser iniciado.   
  
![Gerenciar assinaturas](../reporting-services/media/working-with-subscriptions-web-portal/ssrs-manage-subscriptions.png)  
Acesse a página Assinaturas selecionando as **reticências (...)** de um relatório, selecionando **Gerenciar** e **Assinaturas**.  
  
Na página Assinaturas, você pode criar novas assinaturas selecionando **+ Nova assinatura**. Você também pode editar as assinaturas existentes ou excluir assinaturas que você selecionou.  
  
Essa página também oferece o status do resultado de execuções de assinatura na coluna **Resultado** . Se ocorreu um erro em uma assinatura, primeiro verifique a coluna de resultados para ver a mensagem. 

Você também pode executar uma assinatura sempre que desejar selecionando **Executar agora** na página Assinaturas.
  
## <a name="creating-or-editing-a-subscription"></a>Criar ou editar uma assinatura  
Use a página Nova Assinatura ou Editar Assinatura para criar uma nova assinatura ou editar uma assinatura existente para um relatório. As opções nessa página variam, dependendo de sua atribuição de função. Os usuários com permissões avançadas podem trabalhar com opções adicionais.  
  
As assinaturas têm suporte para relatórios que podem ser executados de modo autônomo. O relatório deve, no mínimo, usar credenciais armazenadas ou nenhuma credencial. Se o relatório usar parâmetros, um valor padrão deverá ser especificado. As assinaturas poderão ficar inativas se você alterar as configurações de execução do relatório ou remover os valores padrão usados por propriedades de parâmetro. Para obter mais informações, confira [Criar e gerenciar assinaturas de servidores de relatório no modo nativo](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md).  
  
## <a name="type-of-subscription"></a>Tipo de assinatura  
Você pode selecionar entre uma **Assinatura padrão** e uma **Assinatura controlada por dados**.  
  
![ssRSWebPortal-subscriptions3](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions3.png)  
   
Uma assinatura controlada por dados é uma assinatura que consulta um banco de dados de assinante para obter informações de assinatura cada vez que a assinatura é executada. Assinaturas controladas por dados usam resultados de consulta para determinar os destinatários da assinatura, as configurações de entrega e os valores de parâmetro do relatório. Em tempo de execução, o servidor de relatórioss executa uma consulta para obter valores usados nas configurações da assinatura.   
  
Para criar uma assinatura controlada por dados, você deve saber como gravar uma consulta ou um comando que obtém os dados para a assinatura. Você também deve ter um armazenamento de dados que contenha os dados do assinante (por exemplo, nomes e endereços de email do assinante) a serem usados na assinatura.  
  
Essa opção está disponível a usuários com permissões avançadas. Se você estiver usando a segurança padrão, as assinaturas controladas por dados não poderão ser usadas nos relatórios da pasta Meus Relatórios.  
  
## <a name="destination"></a>Destino  
Selecione a extensão de entrega a ser usada para distribuir o relatório.   
  
A disponibilidade de uma extensão de entrega depende se ela está instalada e configurada no servidor de relatório. O email do Servidor de Relatório é a extensão de entrega padrão, mas deve ser configurado antes de ser usado. Entrega de Compartilhamento de Arquivo não requer configuração, mas você deve definir uma pasta compartilhada antes de usá-la.  
  
![ssRSWebPortal-subscriptions2](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions2.png)  
  
Dependendo da extensão de entrega selecionada, as configurações a seguir são exibidas:  
  
-   Assinaturas de email fornecem campos que são familiares a usuários de email (por exemplo, os campos Para, Assunto e Prioridade). Especifique **Incluir Relatório** para inserir ou anexar o relatório ou **Incluir Link** para incluir uma URL ao relatório. Especifique **Formato de Renderização** para escolher um formato de apresentação para o relatório anexado ou inserido. Confira [Criar uma assinatura de email](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md#bkmk_create_email_subscription) para obter detalhes. 
  
-   Assinaturas de compartilhamento de arquivo fornecem campos que permitem especificar um local de destino. Você pode entregar qualquer relatório a um compartilhamento de arquivo. No entanto, relatórios que oferecem suporte a recursos interativos (incluindo relatórios matriz com suporte para busca detalhada em linhas e colunas) são renderizados como arquivos estáticos. Você não pode exibir busca detalhada em linhas e colunas em um arquivo estático. O nome do compartilhamento de arquivo deve ser especificado no formato UNC (Convenção de Nomenclatura Uniforme) (por exemplo, \mycomputer\public\myreportfiles). Não inclua barras invertidas à direita no nome do caminho. O arquivo de relatório será entregue em um formato de arquivo que tem base no formato de renderização (por exemplo, se você escolher Excel, o relatório será entregue como um arquivo .xlsx).  Confira [Criar uma assinatura de compartilhamento de arquivo](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md#bkmk_create_fileshare_subscription) para obter detalhes.
  
## <a name="data-driven-subscription-dataset"></a>Conjunto de dados de assinatura controlada por dados  
Para uma assinatura controlada por dados, você precisará definir o conjunto de dados usado para a assinatura. Selecione **Editar conjunto de dados** para fornecer essas informações.  
  
![ssRSWebPortal-subscriptions4](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions4.png)  
  
Primeiro você precisa fornecer uma **fonte de dados** a ser usada na consulta. Pode ser uma fonte de dados compartilhada ou você pode fornecer uma fonte de dados personalizada.  
  
Você precisará, então, fornecer uma **consulta** que listará as diferentes opções necessárias para a execução da assinatura. A tela fornecerá os campos que precisam ser retornados. Esses campos variarão dependendo de seu método de entrega e dos parâmetros do relatório.  
  
Para um resultado melhor, execute a consulta no SQL Server Management Studio primeiro, antes de usá-la na assinatura controlada por dados. Você pode, então, examinar os resultados para verificar se eles contêm as informações necessárias. Pontos importantes a reconhecer sobre os resultados de consulta:  
  
-   As colunas no conjunto de resultados determinam os valores que você pode especificar para opções de entrega e parâmetros do relatório. Por exemplo, se estiver criando uma assinatura controlada por dados para uma entrega de email, você deverá ter uma coluna de endereços de email.  
  
-   Linhas no conjunto de resultados determinam o número de entregas de relatório geradas. Se você tiver 10.000 linhas, o servidor de relatório gerará 10.000 notificações e entregas.  
  
![ssRSWebPortal-subscriptions5](../reporting-services/media/working-with-subscriptions-web-portal/ssrswebportal-subscriptions5.png)  
  
Você pode validar a consulta. Você também pode definir um **tempo limite de consulta**.  
  
Depois que a consulta tiver sido criada, você pode atribuir valores aos campos obrigatórios. Você pode inserir os dados manuais ou selecionar um campo no conjunto de dados que você criou. 

## <a name="next-steps"></a>Próximas etapas

[Criar e gerenciar assinaturas de servidores de relatório no modo nativo](subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md)
[Portal da Web](../reporting-services/web-portal-ssrs-native-mode.md)  
[Trabalhando com relatórios paginados](working-with-paginated-reports-web-portal.md)  
[Trabalhar com conjuntos de dados compartilhados](../reporting-services/work-with-shared-datasets-web-portal.md)

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
