---
description: Novos recursos de GUI no SSMA para DB2 (DB2ToSQL)
title: Novos recursos de GUI no SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a8ed33e9-185a-492d-a4cf-2fded1aa5c70
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d3ad4946b7e900fa9ca4adc22e16a299948e00f9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488147"
---
# <a name="new-gui-features-in-ssma-for-db2-db2tosql"></a>Novos recursos de GUI no SSMA para DB2 (DB2ToSQL)
Este capítulo descreve os novos recursos da interface do usuário do SSMA.  
  
## <a name="layouts"></a>Layouts  
Esse recurso permite que você escolha uma das duas janelas predefinidas de lay-out do Windows ou crie seu próprio layout. Para acessar o submenu layout, no menu Exibir, aponte para layouts. Lá, você pode escolher um dos layouts existentes, adicionar novo layout ou gerenciar layouts.  
  
### <a name="add-current-layout"></a>Adicionar layout atual  
Para salvar o layout atual do Windows, no menu Exibir, aponte para layouts e clique em Adicionar layout atual.  
  
### <a name="choose-predefined-layout"></a>Escolher layout predefinido  
Para escolher um dos layouts predefinidos, no menu Exibir aponte para layouts e clique em layout padrão ou sem Explorers. Você também pode usar atalhos Ctrl + Alt + 1 ou Ctrl + Alt + 2 para layouts predefinidos.  
  
### <a name="choose-user-defined-layout"></a>Escolher layout definido pelo usuário  
Para escolher layout definido pelo usuário, no menu Exibir, aponte para layouts e clique em um dos layouts definidos pelo usuário. Você também pode usar atalhos definidos para os layouts.  
  
### <a name="manage-layouts"></a>Gerenciar layouts  
Para abrir a caixa de diálogo Gerenciar layouts, no menu Exibir, aponte para layouts e clique em gerenciar layouts. Na caixa de diálogo Gerenciar layouts, você encontrará uma lista dos layouts existentes no lado esquerdo da caixa de diálogo. Lá, você pode selecionar o layout para alterar suas configurações. Além disso, você pode alterar a ordem dos layouts na lista ou excluir o layout usando os botões na parte superior da lista. No lado direito da caixa de diálogo, você pode alterar as seguintes configurações de layout:  
  
-   Nome de layout  
  
-   Sincronização de gerenciadores de metadados  
  
-   Visibilidade e largura dos gerenciadores de metadados de origem e de destino  
  
-   Visibilidade das janelas de origem ou de destino e seus tamanhos  
  
-   Visibilidade e altura das janelas auxiliares  
  
## <a name="bookmarks"></a>Indicadores  
Esse recurso permite que você defina um ou mais indicadores no código de origem ou de destino, rapidamente encontrou um indicador usando atalhos, gerenciando os indicadores com uma caixa de diálogo amigável.  
  
### <a name="toggle-bookmark"></a>Ativar/desativar Indicador  
Você pode definir/remover um indicador das seguintes maneiras:  
  
-   Usar indicador de alternância de botão na parte superior da janela SQL de origem ou de destino  
  
-   Clique na área cinza à esquerda da janela SQL  
  
-   Use CTRL + SHIFT + &lt; 0.. 9 &gt; para definir o indicador numerado  
  
### <a name="bookmark-navigation"></a>Navegação por indicadores  
Você pode percorrer os indicadores das seguintes maneiras:  
  
-   Usar botões próximo indicador, indicador anterior na parte superior da janela SQL  
  
-   Use CTRL + &lt; 0.. 9 &gt; para localizar o indicador numerado  
  
-   Usar botões ir para ou exibir origem na caixa de diálogo Gerenciar indicadores  
  
### <a name="removing-bookmark"></a>Removendo indicador  
Você pode remover um indicador das seguintes maneiras:  
  
-   Use o botão limpar na parte superior da janela SQL para remover todos os indicadores no documento atual  
  
-   Usar botões remover ou remover tudo na caixa de diálogo Gerenciar indicadores  
  
### <a name="manage-bookmarks"></a>Gerenciar indicadores  
Para abrir a caixa de diálogo Gerenciar indicadores, no menu Editar, clique em gerenciar indicadores. Na caixa de diálogo, você verá uma lista de indicadores existentes. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.  
  
## <a name="object-history"></a>Histórico de objetos  
O histórico de objetos de GUI permite as seguintes vantagens ao navegar pelos objetos:  
  
-   Você pode usar os botões voltar e avançar para navegar pelos objetos que você já visitou  
  
-   Quando você voltar ao objeto, volte para a mesma guia que você saiu  
  
-   Quando você voltar ao objeto e a guia for SQL, voltará para a mesma posição do cursor que você saiu  
  
## <a name="advanced-search-capabilities"></a>Recursos de pesquisa avançada  
Os recursos de pesquisa avançada fornecem recursos de pesquisa poderosos e flexíveis e permitem localizar a declaração de objeto, obter informações de objeto, executar pesquisa rápida, executar pesquisa avançada de objetos em categorias usando padrões, etc.  
  
### <a name="get-quick-information"></a>Obter informações rápidas  
Você pode obter informações rápidas sobre o objeto na posição do cursor das seguintes maneiras:  
  
-   Clique no botão informações rápidas na parte superior da janela SQL  
  
-   Selecione informações rápidas no menu pop-up clique com o botão direito do mouse  
  
-   Pressione Ctrl + Shift + espaço  
  
### <a name="find-declaration"></a>Declaração de localização  
Você pode ir para a declaração do objeto na posição do cursor das seguintes maneiras:  
  
-   Clique no botão ir para a declaração na parte superior da janela SQL  
  
-   Selecione ir para a declaração no menu pop-up, clique com o botão direito do mouse  
  
-   Pressione F12  
  
### <a name="quick-search"></a>Pesquisa rápida  
Você pode executar a pesquisa de texto rápido usando os seguintes recursos:  
  
-   Você pode iniciar a pesquisa usando o atalho Ctrl + F  
  
-   Você pode repetir a última pesquisa em frente usando F3  
  
-   Você pode repetir a última pesquisa para trás usando Shift + F3  
  
-   Você pode encontrar a próxima ocorrência da palavra na posição do cursor usando Ctrl + F3  
  
-   Você pode encontrar a ocorrência anterior da palavra na posição do cursor usando Ctrl + Shift + F3  
  
-   Você também pode executar todas essas ações com itens de menu.  
  
### <a name="advanced-search"></a>Pesquisa avançada  
Para abrir a caixa de diálogo pesquisa avançada, no menu Editar, aponte para localizar e clique em pesquisa avançada. Na caixa de diálogo, você poderá localizar qualquer objeto usando o padrão. Na parte superior da caixa de diálogo, você pode escolher a área de pesquisa e as categorias de objeto.  
  
