---
title: Criar ou personalizar uma biblioteca de feeds de dados (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data feed library
- data feeds [Analysis Services with SharePoint]
ms.assetid: 699fbeb9-42ab-436b-beba-214db51ea3dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 31e69ddc36079c993e66a7e9253bfdd178057302
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071559"
---
# <a name="create-or-customize-a-data-feed-library-powerpivot-for-sharepoint"></a>Criar ou personalizar uma biblioteca de feed de dados (PowerPivot para SharePoint)
  Uma *biblioteca de feed de dados* é uma biblioteca do SharePoint com finalidade especial que permite registrar e compartilhar documentos do serviço de dados Atom (.atomsvc). Esses documentos fornecem feeds de dados XML a pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ou outros aplicativos cliente que oferecem suporte ao formato de feed de dados Atom. Uma biblioteca de feeds de dados é diferente de outras bibliotecas do SharePoint porque oferece a capacidade de:  
  
-   Criar ou editar um *documento do serviço de dados*usado para especificar uma conexão HTTP com um feed específico.  
  
-   Compartilhar e gerenciar documentos do serviço de dados em um local central.  
  
-   Identificar visualmente documentos do serviço de dados por um ícone, de forma que você possa distinguir facilmente documentos do serviço de outros documentos armazenados na mesma biblioteca: ![GMNI_IconDataFeed](../media/gmni-icondatafeed.gif "GMNI_IconDataFeed")  
  
 Uma biblioteca de feeds de dados sempre contém arquivos de documento do serviço de dados (.atomsvc) e nunca o próprio feed de dados. Ao contrário de um feed de dados, que consiste em dados XML estáticos, o documento do serviço de dados especifica uma URL para um serviço ou aplicativo que gera um feed sob solicitação, fornecendo informações de conexão reutilizáveis para operações de importação repetíveis.  
  
 Este tópico contém as seguintes seções:  
  
 [Pré-requisitos](#prereq)  
  
 [Criar uma nova biblioteca de feeds de dados](#createlib)  
  
 [Adicionar o tipo de conteúdo do feed de dados a uma biblioteca](#addtolib)  
  
##  <a name="prereq"></a> Pré-requisitos  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] deve ser ativada para sites para os quais você está criando a biblioteca de feeds de dados. Se o tipo de modelo da biblioteca de feeds de dados não estiver disponível, a causa mais provável será que esse pré-requisito não foi atendido. Para obter mais informações, consulte [ativar a integração do recurso do PowerPivot para coleções de sites na Administração Central](activate-power-pivot-integration-for-site-collections-in-ca.md).  
  
 Você deve ser um proprietário do site criar a biblioteca.  
  
##  <a name="createlib"></a> Criar uma nova biblioteca de feeds de dados  
 A criação de uma biblioteca de feeds de dados é a primeira etapa para habilitar feeds de dados para pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Como uma biblioteca de feeds de dados fornece páginas de aplicativo e gerenciamento para os documentos do serviço de dados, você deve ter essa biblioteca pronta para criar um novo documento.  
  
 Uma biblioteca de feeds de dados é baseada em um modelo interno e em um *tipo de conteúdo de documento do serviço de dados* pré-configurado que define propriedades e comportamentos para um documento do serviço de dados.  
  
1.  Clique em **Ações do Site** no canto superior esquerdo da página.  
  
2.  Clique em **mais opções**...  
  
3.  Em Bibliotecas, clique em **Biblioteca de Feeds de Dados**.  
  
4.  Digite o nome, a descrição e as preferências de inicialização e versão. Inclua informações descritivas para ajudar os usuários a identificarem essa biblioteca como armazenamento para documentos do serviço de dados.  
  
5.  Clique em **Criar**.  
  
 Um link para a biblioteca de feeds de dados é exibido no painel Início Rápido da navegação do site atual.  
  
 Depois de criar uma biblioteca, você pode usá-la para criar documentos de serviço de dados. Para obter mais informações, consulte [usar Feeds de dados &#40;PowerPivot para SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md).  
  
##  <a name="addtolib"></a> Adicionar o tipo de conteúdo do feed de dados a uma biblioteca  
 Se você não desejar criar uma biblioteca de feeds de dados dedicada, mas ainda quiser criar e gerenciar documentos do serviço de dados de um site do SharePoint, poderá adicionar e configurar manualmente o tipo de conteúdo de documento do serviço de dados para qualquer biblioteca que será usada para compartilhar arquivos de documento do serviço de dados (.atomsvc).  
  
 Você deve ter pelo menos a permissão Gerenciar Listas para adicionar e configurar um tipo de conteúdo. Esta permissão é compilada no nível de permissão Design e superior.  
  
 As etapas a seguir devem ser repetidas para cada biblioteca na qual você deseja criar ou editar documentos de registro de feed de dados.  
  
#### <a name="step-1-enable-content-type-management"></a>Etapa 1: Habilitar o gerenciamento de tipo de conteúdo  
  
1.  Abra a biblioteca de documentos para a qual você deseja habilitar vários tipos de conteúdo.  
  
2.  Na faixa de opções do SharePoint, em Ferramentas de Biblioteca, clique em **Biblioteca**.  
  
3.  Clique em **Configurações**.  
  
4.  Clique em **Configurações da Biblioteca**.  
  
5.  Em Configurações Gerais, clique em **Configurações avançadas**.  
  
6.  Em Tipos de Conteúdo, na seção "Permitir o gerenciamento de tipos de conteúdo?", clique em **Sim**.  
  
7.  Clique em **OK**.  
  
#### <a name="step-2-add-the-data-service-document-content-type"></a>Etapa 2: Adicione o tipo de conteúdo do documento de serviço de dados  
  
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
 [Usar Feeds de dados &#40;PowerPivot para SharePoint&#41;](use-data-feeds-power-pivot-for-sharepoint.md)   
 [Excluir uma biblioteca de feeds de dados do PowerPivot](delete-a-power-pivot-data-feed-library.md)   
 [Administração de servidor do PowerPivot e a configuração na Administração Central](power-pivot-server-administration-and-configuration-in-central-administration.md)   
 [Feeds de dados PowerPivot](power-pivot-data-feeds.md)  
  
  
