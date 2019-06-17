---
title: Novos recursos de GUI no SSMA para Oracle (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 62e2d30f-a73f-42d9-a6ab-3510a8198f4e
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: ee8637bb85c390378dc5c886165ddfa12950e03b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209823"
---
# <a name="new-gui-features-in-ssma-for-oracle-oracletosql"></a>Novos recursos de GUI no SSMA para Oracle (OracleToSQL)
Este capítulo descreve os novos recursos da Interface de usuário do SSMA.  
  
## <a name="layouts"></a>Layouts  
Esse recurso permite que você escolha uma das duas janelas predefinidas dispor ou crie sua própria layout. Para acessar o submenu de layout, no menu Exibir, aponte para Layouts. Lá você pode escolher um dos layouts existentes, adicione o novo layout ou gerenciar layouts.  
  
### <a name="add-current-layout"></a>Adicionar o Layout atual  
Para salvar o layout atual do windows, no menu Exibir, aponte para Layouts e clique em Adicionar Layout atual.  
  
### <a name="choose-predefined-layout"></a>Escolha o layout predefinido  
Para escolher um dos layouts predefinidos, no menu Exibir, aponte para Layouts e clique em Layout padrão ou sem Explorers. Você também pode usar atalhos de Ctrl + Alt + 1 ou Ctrl + Alt + 2 para layouts predefinidos.  
  
### <a name="choose-user-defined-layout"></a>Escolher o layout definido pelo usuário  
Para escolher o layout definido pelo usuário, no menu Exibir, aponte para Layouts e clique em um do layout definido pelo usuário. Você também pode usar atalhos definidos para os layouts.  
  
### <a name="manage-layouts"></a>Gerenciar layouts  
Para abrir a caixa de diálogo Gerenciar Layouts, no menu Exibir, aponte para Layouts e clique em Gerenciar Layouts. Na caixa de diálogo Gerenciar Layouts, você encontrará uma lista dos layouts existentes no lado esquerdo da caixa de diálogo. Lá você pode selecionar o layout para alterar suas configurações. Também pode alterar a ordem de layouts na lista ou excluir o layout usando os botões na parte superior da lista. No lado direito da caixa de diálogo, você pode alterar as configurações de layout a seguir:  
  
-   Nome do layout  
  
-   Sincronização de gerenciadores de metadados  
  
-   Visibilidade e a largura dos exploradores de metadados de origem e destino  
  
-   Visibilidade das janelas de origem ou destino e seus tamanhos  
  
-   Visibilidade e a altura do windows auxiliares  
  
## <a name="bookmarks"></a>Indicadores  
Esse recurso permite que você defina um ou mais indicadores na fonte ou código de destino, o rápido encontrado um indicador usando atalhos, gerenciar indicadores com uma caixa de diálogo amigável.  
  
### <a name="toggle-bookmark"></a>Toggle Bookmark  
Você pode definir/remover o indicador das seguintes maneiras:  
  
-   Use o botão Ativar/Desativar indicador na parte superior da janela SQL de origem ou destino  
  
-   Clique na área cinza à esquerda da janela SQL  
  
-   Use Ctrl + Shift +&lt;0..9&gt; para definir um indicador numerado  
  
### <a name="bookmark-navigation"></a>Navegação por indicadores  
Você pode orientá-lo thru indicadores das seguintes maneiras:  
  
-   Use os botões Próximo indicador, o indicador anterior na parte superior da janela SQL  
  
-   Use Ctrl +&lt;0..9&gt; para encontrar o indicador numerado  
  
-   Use os botões Ir para ou exibir código-fonte na caixa de diálogo Gerenciar indicadores  
  
### <a name="removing-bookmark"></a>Removendo o indicador  
Você pode remover um indicador das seguintes maneiras:  
  
-   Use o botão Limpar na parte superior da janela SQL para remover todos os indicadores no documento atual  
  
-   Use os botões Remover ou remover tudo na caixa de diálogo Gerenciar indicadores  
  
### <a name="manage-bookmarks"></a>Gerenciar indicadores  
Para abrir a caixa de diálogo Gerenciar indicadores, no menu Editar, clique em Gerenciar indicadores. Na caixa de diálogo, você verá uma lista de indicadores atuais. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.  
  
## <a name="object-history"></a>Histórico de objeto  
Histórico de GUI do objeto permite que você as seguintes vantagens ao navegar objetos:  
  
-   Você pode usar botões Voltar e Avançar para navegar os objetos que você já tenha visitado  
  
-   Quando você de volta para o objeto, você de volta para a mesma guia que você tenha deixado  
  
-   Quando você volta para o objeto e a guia é SQL, você volta para a mesma posição de cursor que você tenha deixado  
  
## <a name="advanced-search-capabilities"></a>Recursos avançados de pesquisa  
Recursos avançados de pesquisa fornecem os recursos de pesquisando poderosos e flexíveis e permitem que você localize a declaração de objeto, obter informações do objeto, realizar a pesquisa rápida, executar objetos avançada pesquisando em categorias usando padrões etc.  
  
### <a name="get-quick-information"></a>Obter informações rápidas  
Você pode obter informações rápidas sobre o objeto na posição do cursor das seguintes maneiras:  
  
-   Clique o botão informações rápidas na parte superior da janela SQL  
  
-   Selecione informações rápidas no menu pop-up do mouse  
  
-   Pressione Ctrl + Shift + espaço  
  
### <a name="find-declaration"></a>Localize a declaração  
Você pode ir para a declaração do objeto na posição do cursor das seguintes maneiras:  
  
-   Clique em Ir para declaração de botão na parte superior da janela SQL  
  
-   Selecione Ir para declaração no menu pop-up do mouse  
  
-   Pressione F12  
  
### <a name="quick-search"></a>Pesquisa rápida  
Você pode executar a pesquisa de texto rápido usando os seguintes recursos:  
  
-   Você pode iniciar a pesquisa usando o atalho Ctrl + F  
  
-   Você pode repetir a última pesquisa para frente usando F3  
  
-   Você pode repetir a última pesquisa com versões anteriores, usando Shift + F3  
  
-   Você pode encontrar a próxima ocorrência da palavra na posição do cursor usando Ctrl + F3  
  
-   Você pode localizar a ocorrência anterior da palavra na posição do cursor usando Ctrl + Shift + F3  
  
-   Você também pode executar todas essas ações com itens de menu.  
  
### <a name="advanced-search"></a>Pesquisa avançada  
Para abrir a caixa de diálogo de pesquisa avançada, no menu Editar ponto de localizar, em seguida, clique em pesquisa avançada. Na caixa de diálogo, você poderá localizar qualquer objeto usando o padrão. Na parte superior da caixa de diálogo, você pode escolher categorias de objeto e de área de pesquisa.  
  
