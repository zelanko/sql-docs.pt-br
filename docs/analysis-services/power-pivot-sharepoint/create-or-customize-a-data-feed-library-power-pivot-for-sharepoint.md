---
title: Criar ou personalizar uma biblioteca de Feed de dados (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data feed library
- data feeds [Analysis Services with SharePoint]
ms.assetid: 699fbeb9-42ab-436b-beba-214db51ea3dd
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 55a0d510b8d80ca4c3752194b4c9c488ac4d787b
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="create-or-customize-a-data-feed-library-power-pivot-for-sharepoint"></a>Criar ou personalizar uma biblioteca de feed de dados (Power Pivot para SharePoint)
  Uma *biblioteca de feed de dados* é uma biblioteca do SharePoint com finalidade especial que permite registrar e compartilhar documentos do serviço de dados Atom (.atomsvc). Esses documentos fornecem feeds de dados XML a pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou outros aplicativos cliente que oferecem suporte ao formato de feed de dados Atom. Uma biblioteca de feeds de dados é diferente de outras bibliotecas do SharePoint porque oferece a capacidade de:  
  
-   Criar ou editar um *documento do serviço de dados*usado para especificar uma conexão HTTP com um feed específico.  
  
-   Compartilhar e gerenciar documentos do serviço de dados em um local central.  
  
-   Identificar visualmente documentos do serviço de dados por um ícone, para que você possa distinguir facilmente documentos do serviço de outros documentos armazenados na mesma biblioteca: ![GMNI_IconDataFeed](../../analysis-services/power-pivot-sharepoint/media/gmni-icondatafeed.gif "GMNI_IconDataFeed")  
  
 Uma biblioteca de feeds de dados sempre contém arquivos de documento do serviço de dados (.atomsvc) e nunca o próprio feed de dados. Ao contrário de um feed de dados, que consiste em dados XML estáticos, o documento do serviço de dados especifica uma URL para um serviço ou aplicativo que gera um feed sob solicitação, fornecendo informações de conexão reutilizáveis para operações de importação repetíveis.  
  
 Este tópico contém as seguintes seções:  
  
 [Pré-requisitos](#prereq)  
  
 [Criar uma nova biblioteca de feeds de dados](#createlib)  
  
 [Adicionar o tipo de conteúdo do feed de dados a uma biblioteca](#addtolib)  
  
##  <a name="prereq"></a> Pré-requisitos  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] deve ser ativada para sites para os quais você está criando a biblioteca de feeds de dados. Se o tipo de modelo da biblioteca de feeds de dados não estiver disponível, a causa mais provável será que esse pré-requisito não foi atendido. Para obter mais informações, consulte [Activate Power Pivot Feature Integration for Site Collections in Central Administration](../../analysis-services/power-pivot-sharepoint/activate-power-pivot-integration-for-site-collections-in-ca.md).  
  
 Você deve ser um proprietário do site criar a biblioteca.  
  
##  <a name="createlib"></a> Criar uma nova biblioteca de feeds de dados  
 A criação de uma biblioteca de feeds de dados é a primeira etapa para habilitar feeds de dados para pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Como uma biblioteca de feeds de dados fornece páginas de aplicativo e gerenciamento para os documentos do serviço de dados, você deve ter essa biblioteca pronta para criar um novo documento.  
  
 Uma biblioteca de feeds de dados é baseada em um modelo interno e em um *tipo de conteúdo de documento do serviço de dados* pré-configurado que define propriedades e comportamentos para um documento do serviço de dados.  
  
1.  Clique em **Ações do Site** no canto superior esquerdo da página.  
  
2.  Clique em **Mais Opções**…  
  
3.  Em Bibliotecas, clique em **Biblioteca de Feeds de Dados**.  
  
4.  Digite o nome, a descrição e as preferências de inicialização e versão. Inclua informações descritivas para ajudar os usuários a identificarem essa biblioteca como armazenamento para documentos do serviço de dados.  
  
5.  Clique em **Criar**.  
  
 Um link para a biblioteca de feeds de dados é exibido no painel Início Rápido da navegação do site atual.  
  
 Depois de criar uma biblioteca, você pode usá-la para criar documentos de serviço de dados. Para obter mais informações, consulte [Use feeds de dados &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="addtolib"></a> Adicionar o tipo de conteúdo do feed de dados a uma biblioteca  
 Se você não desejar criar uma biblioteca de feeds de dados dedicada, mas ainda quiser criar e gerenciar documentos do serviço de dados de um site do SharePoint, poderá adicionar e configurar manualmente o tipo de conteúdo de documento do serviço de dados para qualquer biblioteca que será usada para compartilhar arquivos de documento do serviço de dados (.atomsvc).  
  
 Você deve ter pelo menos a permissão Gerenciar Listas para adicionar e configurar um tipo de conteúdo. Esta permissão é compilada no nível de permissão Design e superior.  
  
 As etapas a seguir devem ser repetidas para cada biblioteca na qual você deseja criar ou editar documentos de registro de feed de dados.  
  
#### <a name="step-1-enable-content-type-management"></a>Etapa 1: Habilitar o gerenciamento do tipo de conteúdo  
  
1.  Abra a biblioteca de documentos para a qual você deseja habilitar vários tipos de conteúdo.  
  
2.  Na faixa de opções do SharePoint, em Ferramentas de Biblioteca, clique em **Biblioteca**.  
  
3.  Clique em **Configurações**.  
  
4.  Clique em **Configurações da Biblioteca**.  
  
5.  Em Configurações Gerais, clique em **Configurações avançadas**.  
  
6.  Em Tipos de Conteúdo, na seção "Permitir o gerenciamento de tipos de conteúdo?", clique em **Sim**.  
  
7.  Clique em **OK**.  
  
#### <a name="step-2-add-the-data-service-document-content-type"></a>Etapa 2: Adicionar o tipo de conteúdo de documento de serviço de dados  
  
1.  Na seção Tipos de Conteúdo, clique em **Adicionar a partir de tipos de conteúdo de site existentes**. Se você não vir essa página, volte para o site, clique em **Biblioteca** em Ferramentas de Biblioteca e clique em **Definições da Biblioteca**.  
  
2.  Em Tipos de Conteúdo, clique em **Adicionar a partir de tipos de conteúdo de site existentes**.  
  
3.  Em Selecionar tipos de conteúdo de site de:, selecione **Business Intelligence**.  
  
4.  Em Tipos Disponíveis de Conteúdo do Site, clique em **Documento de Serviço de Dados**e clique em **Adicionar** para mover o tipo de conteúdo selecionado para a lista Tipos de conteúdo a serem adicionados.  
  
5.  Clique em **OK**.  
  
#### <a name="step-3-verify-data-service-document-configuration"></a>Etapa 3: Verificar a configuração do documento de serviço de dados  
  
1.  Abra a página inicial do site.  
  
2.  Abra a biblioteca.  
  
3.  Na faixa de opções do SharePoint, clique em **Documentos**.  
  
4.  Clique na seta para baixo em Novo Documento e selecione **Documento de Serviço de Dados**. A página Novo Documento de Serviço de Dados deve aparecer.  
  
## <a name="see-also"></a>Consulte também  
 [Use feeds de dados &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/use-data-feeds-power-pivot-for-sharepoint.md)   
 [Excluir uma biblioteca de Feed de dados do Power Pivot](../../analysis-services/power-pivot-sharepoint/delete-a-power-pivot-data-feed-library.md)   
 [Administração e configuração de servidor do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Feeds de dados do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-feeds.md)  
  
  
