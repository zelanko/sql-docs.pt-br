---
title: Página de pesquisa (Report Manager) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 51ffdc07-e1b9-4ed7-acb3-dd98d7cce273
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 12413c103230d8c085a9701e3fb83db15135895a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102257"
---
# <a name="search-page-report-manager"></a>Página Pesquisa (Gerenciador de Relatórios)
  Use a página Resultados da Pesquisa para exibir os resultados de uma operação de pesquisa especificada para um relatório, relatório vinculado, modelo de relatório, fonte de dados compartilhada, pasta ou recurso. Os resultados da pesquisa são listados em ordem alfabética. Você pode classificar por tipo, nome ou descrição.  
  
 Os itens a seguir são excluídos de uma operação de pesquisa: instantâneos de relatório contidos em histórico de relatório, assinatura e agendas compartilhadas. Da mesma forma, permissão não adequada para exibir uma pasta ou um relatório exclui aquele item de uma pesquisa.  
  
 Você não pode procurar texto dentro de um relatório ou modelo. Para procurar um texto específico em um relatório, use a barra de ferramentas na parte superior do relatório.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-search-results-page"></a>Para abrir a página Resultados da Pesquisa  
  
1.  Abra o Gerenciador de Relatórios.  
  
2.  Na parte superior da página, digite os critérios de pesquisa na caixa **Pesquisar**. Em seguida, pressione Enter ou clique na seta Pesquisar.  
  
## <a name="options"></a>Opções  
 **Delete (excluir)**  
 Clique para remover um item de um banco de dados do servidor de relatório.  
  
> [!NOTE]  
>  Este botão só está disponível em **Exibição de Detalhes**. Porém, você pode focalizar um item e usar o menu para acessar a funcionalidade de exclusão em **Exibição de Detalhes** ou em **Exibição de Lista**.  
  
 **Mover**  
 Clique para realocar um item. Isso abre a página Mover Itens, onde você pode selecionar um local de pasta diferente.  
  
> [!NOTE]  
>  Este botão só está disponível em **Exibição de Detalhes**. Porém, você pode focalizar um item e usar o menu para acessar a funcionalidade de movimentação em **Exibição de Detalhes** ou em **Exibição de Lista**.  
  
 Caixa de pesquisa  
 Digite todo ou parte do nome de um item que você deseja localizar e clique em **Ir** para iniciar a pesquisa. A cadeia de caracteres mais longa que você pode pesquisar é de 128 caracteres.  
  
 Nomes de itens ou descrições que contêm toda a cadeia de caracteres da pesquisa em qualquer lugar do valor de texto serão incluídos nos resultados da pesquisa.  
  
 Os operadores boolianos como o caractere de adição (+) não têm suporte.  
  
 **Exibição de Detalhes**  
 Clique para exibir a página Resultados da Pesquisa em uma lista que contém informações adicionais sobre os itens, como o tipo de item, o nome, a descrição, a pasta na qual o item está localizado e quando ele foi executado pela última vez. Em **Exibição de Detalhes**, é possível usar os botões **Excluir** e **Mover** para remover e realocar itens na pasta.  
  
 Focalize um item e clique na seta do menu suspenso para abri-lo e acessar e configurar as propriedades do item selecionado.  
  
 **Exibição de lista**  
 Clique para exibir a página Resultados da Pesquisa sem os detalhes da **Exibição de Detalhes**. Exibição de Lista é a exibição padrão quando a página Resultados da Pesquisa é exibida.  
  
 Focalize um item e clique na seta do menu suspenso para abri-lo e acessar e configurar as propriedades do item selecionado.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
