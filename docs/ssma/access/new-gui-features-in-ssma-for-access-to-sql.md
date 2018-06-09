---
title: Novos recursos de interface gráfica do usuário do SSMA para Access para o SQL | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 95b95de2-db05-4422-825d-43968ecfd01c
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c85cd4e2cade37e20549aeaf76e94efd3224fad1
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34774742"
---
# <a name="new-gui-features-in-ssma-for-access-to-sql"></a>Novos recursos de interface gráfica do usuário do SSMA para Access to SQL
Este capítulo descreve novos recursos da Interface de usuário do SSMA  
  
## <a name="layouts"></a>Layouts  
Esse recurso permite que você escolha uma das duas janelas predefinidas dispor ou criar seu próprio layout. Para acessar o submenu de layout, no menu Exibir, aponte para Layouts. Lá você pode escolher um dos layouts existentes, adicione o layout atual ou gerenciar layouts.  
  
### <a name="add-current-layout"></a>Adicionar o Layout atual  
Para salvar o layout atual do windows, no menu Exibir, aponte para Layouts e clique em Adicionar Layout atual.  
  
### <a name="choose-predefined-layout"></a>Escolha o layout predefinido  
Para escolher um dos layouts predefinidos, no menu Exibir, aponte para Layouts e clique em Layout padrão ou sem pesquisadores. Você também pode usar atalhos Ctrl + Alt + 1 ou Ctrl + Alt + 2 para layouts predefinidos respectivamente.  
  
### <a name="choose-user-defined-layout"></a>Escolha o layout definido pelo usuário  
Para escolher o layout definido pelo usuário, no menu Exibir, aponte para Layouts e clique em um layout definidas pelo usuário. Você também pode usar os atalhos definidos para os layouts.  
  
### <a name="manage-layouts"></a>Gerenciar layouts  
Para abrir a caixa de diálogo Gerenciar Layouts, no menu Exibir, aponte para Layouts e clique em Gerenciar Layouts. Na caixa de diálogo Gerenciar Layouts, você encontrará uma lista dos layouts existentes no lado esquerdo da caixa de diálogo. Lá você pode selecionar o layout para alterar suas configurações. Também pode alterar a ordem de layouts na lista ou excluir o layout usando os botões na parte superior da lista. No lado direito da caixa de diálogo, você pode alterar as seguintes configurações de layout:  
  
-   Nome de layout  
  
-   Sincronização de pesquisadores de metadados  
  
-   Visibilidade e a largura de gerenciadores de metadados de origem e destino  
  
-   Visibilidade de seus tamanhos e as janelas de origem ou de destino  
  
-   Visibilidade e a altura do windows auxiliares  
  
## <a name="bookmarks"></a>Indicadores  
Esse recurso permite que você defina um ou mais indicadores na fonte ou código de destino, rápido encontrou um indicador usando atalhos, gerenciar os indicadores com uma caixa de diálogo amigável.  
  
### <a name="toggle-bookmark"></a>Ativar/Desativar indicador  
Você pode definir ou remover o indicador das seguintes maneiras:  
  
-   Use o botão Ativar/Desativar indicador na parte superior da janela SQL de origem ou de destino  
  
-   Clique na área cinza à esquerda da janela do SQL  
  
-   Use Ctrl + Shift +&lt;0..9&gt; para definir o indicador numerado  
  
### <a name="bookmark-navigation"></a>Navegação de indicador  
Você pode ir até os indicadores das seguintes maneiras:  
  
-   Use os botões Próximo indicador, o indicador anterior na parte superior da janela do SQL  
  
-   Use Ctrl +&lt;0..9&gt; para localizar o indicador numerado  
  
-   Use os botões Ir para ou exibir código-fonte na caixa de diálogo Gerenciar indicadores  
  
### <a name="removing-bookmark"></a>Removendo o indicador  
Você pode remover um indicador das seguintes maneiras:  
  
-   Use o botão Limpar na parte superior da janela do SQL para remover todos os indicadores no documento atual  
  
-   Use os botões Remover ou remover tudo na caixa de diálogo Gerenciar indicadores  
  
### <a name="manage-bookmarks"></a>Gerenciar indicadores  
Para abrir a caixa de diálogo Gerenciar indicadores, no menu Editar, clique em Gerenciar indicadores. Na caixa de diálogo, você verá uma lista de indicadores. Você pode usar os botões à direita da caixa de diálogo para gerenciar os indicadores.  
  
## <a name="object-history"></a>Histórico de objeto  
Histórico de GUI do objeto permite as seguintes vantagens ao navegar objetos:  
  
-   Você pode usar os botões Voltar e Avançar para navegar os objetos que você visitou  
  
-   Quando você de volta para o objeto, você de volta para a guia mesmo que você deixou  
  
-   Quando você volta para o objeto e a guia é SQL, você de volta para a mesma posição de cursor que você deixou  
  
## <a name="advanced-search-capabilities"></a>Recursos avançados de pesquisa  
Recursos avançados de pesquisa fornecem os recursos de pesquisando poderoso e flexíveis e permitem que você encontrar a declaração do objeto, obter informações do objeto, executar pesquisa rápida, executar o objeto avançado pesquisando em categorias usando padrões etc.  
  
### <a name="get-quick-information"></a>Obter informações rápidas  
Você pode obter informações rápidas sobre o objeto na posição do cursor das seguintes maneiras:  
  
-   Clique o botão informações rápidas na parte superior da janela do SQL  
  
-   Selecione informações rápidas no menu pop-up de atalho  
  
-   Pressione Ctrl + Shift + espaço  
  
### <a name="find-declaration"></a>Localizar declaração  
Você pode ir para a declaração do objeto na posição do cursor das seguintes maneiras:  
  
-   Botão Ir para a declaração acima da janela SQL  
  
-   Selecione Ir para declaração no menu pop-up de atalho  
  
-   Pressione a tecla F12  
  
### <a name="quick-search"></a>Pesquisa rápida  
Você pode executar a pesquisa de texto rápida usando os seguintes recursos:  
  
-   Você pode iniciar a pesquisa usando o atalho Ctrl + F  
  
-   Você pode repetir a última pesquisa forward usando F3  
  
-   Você pode repetir a última pesquisa para trás usando Shift + F3  
  
-   Você pode encontrar a próxima ocorrência da palavra na posição do cursor usando Ctrl + F3  
  
-   Você pode localizar a ocorrência anterior da palavra na posição do cursor usando Ctrl + Shift + F3  
  
-   Você também pode executar todas essas ações com itens de menu.  
  
### <a name="advanced-search"></a>Pesquisa avançada  
Para abrir a caixa de diálogo de pesquisa avançada, no menu Editar ponto localizar, em seguida, clique em pesquisa avançada. Na caixa de diálogo, você poderá encontrar qualquer objeto usando o padrão. Na parte superior da caixa de diálogo, você pode escolher categorias de objeto e de área de pesquisa.  
  
