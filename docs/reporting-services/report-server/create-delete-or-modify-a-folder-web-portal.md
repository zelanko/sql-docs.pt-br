---
title: Criar, excluir ou modificar uma pasta – Reporting Services | Microsoft Docs
description: Saiba como criar, modificar e excluir pastas para que você possa organizar e gerenciar os itens publicados em um servidor de relatório do Reporting Services.
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 70a38879-856c-414b-8479-5f9dead38f15
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ae3ae4b181ee6b3308bcbe5bcfc4af1ca370c974
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84548018"
---
# <a name="create-delete-or-modify-a-folder---reporting-services"></a>Criar, excluir ou modificar uma pasta – Reporting Services
  É possível criar pastas para organizar e administrar os itens publicados em um servidor de relatório. Criar pastas pode ajudar os usuários a localizar relatórios de seu interesse. Para gerenciadores de conteúdo, pastas fornecem uma estrutura para a aplicação de permissões. É possível criar atribuições de função em pastas específicas para restringir o acesso a relatórios em desenvolvimento ou que não devem ser distribuídos amplamente.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="to-create-a-folder"></a>Para criar uma pasta  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  No Gerenciador de Relatórios, selecione a pasta Base e clique em **Nova Pasta**. Ou, para criar uma pasta na pasta já existente, navegue até essa pasta na página **Conteúdo** e clique na pasta para abri-la. Clique em **Nova Pasta**.  
  
     A página **Nova Pasta** será aberta.  
  
3.  Digite um nome de pasta. Um nome de pasta pode incluir espaços, mas não pode incluir caracteres reservados usados para codificação de URL: \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. Não é possível digitar uma série de nomes de pasta para criar várias pastas de uma vez.  
  
4.  Como opção, digite uma descrição.  
  
5.  Selecione **Ocultar na exibição de lista** se não deseja exibir a pasta na exibição padrão da página **Conteúdo** . A pasta só será visível a usuários quando eles clicarem em **Mostrar Detalhes** na página **Conteúdo** .  
  
6.  Clique em **OK**.  
  
## <a name="to-delete-a-folder"></a>Para excluir uma pasta  
  
1.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** e localize o item que você deseja modificar.  
  
2.  Focalize o item e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Excluir**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-modify-or-delete-a-folder"></a>Para modificar ou excluir uma pasta  
  
1.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** e localize o item que você deseja modificar.  
  
2.  Focalize o item e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. A página Propriedades Gerais será aberta.  
  
4.  Para alterar o local da pasta, clique em **Mover**. Digite o local da pasta de destino ou escolha a pasta de destino da árvore e clique em **OK**.  
  
5.  Ou modifique as propriedades de pasta das seguintes maneiras:  
  
    -   Para modificar o texto de exibição sobre a pasta, digite um nome ou descrição.  
  
    -   Para exibir a pasta na exibição padrão na página **Conteúdo** , desmarque **Ocultar na exibição de lista**.  
  
6.  Ou, para remover a pasta e seu conteúdo, clique em **Excluir**.  
  
7.  Clique em **Aplicar** para salvar os detalhes.  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
 
## <a name="to-create-a-folder"></a>Para criar uma pasta  
  
1. Abra [o portal da Web de um servidor de relatório (Modo Nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
2. Navegue até a pasta ou subpasta na qual você deseja colocar a nova pasta. Selecione a pasta **Página Inicial** selecionando o botão **Procurar** na barra de ferramentas na parte superior esquerda da página para criá-la na parte superior da hierarquia de pastas.  
  
3. Selecione o botão **Novo** na parte superior direita da barra de ferramentas do servidor de relatório e selecione **Pasta** no menu suspenso.  
  
4. Na caixa de diálogo **Criar uma nova pasta em (nome da pasta atual)** , digite o nome da nova pasta a ser criada. Um nome de pasta pode incluir espaços, mas não pode incluir caracteres reservados para uso na codificação de URL: \;\? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. Você também não pode digitar uma série de nomes de pasta para criar várias pastas de uma vez.  
  
5. Selecione **Criar** para concluir a ação.  
  
## <a name="to-delete-a-folder"></a>Para excluir uma pasta  
  
1. No portal da Web, navegue na hierarquia de pastas e localize a pasta a excluir.  
  
2. Clique com o botão direito do mouse na pasta e selecione **Excluir** no menu suspenso.  
  
3. Selecione o botão **Excluir** na caixa de diálogo **Excluir <foldername>**  para confirmar a exclusão.  
  
## <a name="to-modify-a-folders-properties"></a>Para modificar as propriedades de uma pasta  
  
1. No portal da Web, navegue na hierarquia de pastas e localize a pasta a excluir.  
  
2. Clique com o botão direito do mouse na pasta e selecione **Excluir** no menu suspenso.  
  
3. Clique na guia **Propriedades**. A página **Propriedades** é exibida por padrão.  
  
4. Você pode alterar o nome da pasta na caixa de texto *Nome**.  
  
5. Você pode adicionar ou alterar a descrição da pasta na caixa de texto *Descrição**.  
  
6. Você pode ocultar ou cancelar a ocultação da pasta respectivamente marcando ou desmarcando a caixa de seleção **Ocultar este item**.  
  
7. Selecione **Aplicar** para salvar as alterações de propriedades.  
  
8. Opcionalmente, mova ou exclua a pasta selecionando os botões **Mover** ou **Excluir** na parte superior da página **Propriedades**. Confira mais informações no artigo [Mover ou excluir um item (portal da Web)](../../reporting-services/report-server/move-or-delete-an-item-report-manager.md).  
  
## <a name="see-also"></a>Confira também  
 [Criar, excluir ou modificar uma pasta (portal da Web)](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)   
 [Gerenciamento do conteúdo do servidor de relatório (Modo Nativo SSRS)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)    
  
::: moniker-end