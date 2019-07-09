---
title: Criar, excluir ou modificar uma pasta - Reporting Services | Microsoft Docs
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 70a38879-856c-414b-8479-5f9dead38f15
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 874fb7ba143c8f08a0f25501e1852b4d2b280cb2
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492852"
---
# <a name="create-delete-or-modify-a-folder---reporting-services"></a>Criar, excluir ou modificar uma pasta - Reporting Services
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
  
7.  Clique em **Aplicar** para salvar as alterações.  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
 
## <a name="to-create-a-folder"></a>Para criar uma pasta  
  
1. Abra [o portal da Web de um servidor de relatório (Modo Nativo do SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
2. Navegue até a pasta ou subpasta onde você deseja localizar a nova pasta. Selecione o **página inicial** pasta selecionando o **procurar** na barra de ferramentas na parte superior esquerda da página para criá-lo na parte superior da hierarquia de pastas.  
  
3. Selecione o **New** botão na parte superior direita da barra de ferramentas de servidor de relatório e, em seguida, selecione **pasta** no menu suspenso.  
  
4. No **criar uma nova pasta (nome da pasta atual)** caixa de diálogo, digite o nome da nova pasta a ser criado. Um nome de pasta pode incluir espaços, mas não pode incluir caracteres reservados usados para codificação de URL: \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. Você também não pode digitar uma série de nomes de pasta para criar várias pastas de uma vez.  
  
5. Selecione **criar** para concluir a ação.  
  
## <a name="to-delete-a-folder"></a>Para excluir uma pasta  
  
1. No portal da web, navegar na hierarquia de pasta e localize a pasta que você deseja excluir.  
  
2. Direito-click-a pasta e selecione **excluir** no menu suspenso.  
  
3. Selecione o **exclua** botão na **excluir <foldername>**  caixa de diálogo para confirmar a exclusão.  
  
## <a name="to-modify-a-folders-properties"></a>Para modificar as propriedades de uma pasta  
  
1. No portal da web, navegar na hierarquia de pasta e localize a pasta que você deseja excluir.  
  
2. Direito-click-a pasta e selecione **excluir** no menu suspenso.  
  
3. Selecione a guia **Propriedades**. O **propriedades** página é exibida por padrão.  
  
4. Você pode alterar o nome da pasta na *nome** caixa de texto.  
  
5. Você pode adicionar ou alterar a descrição da pasta na *descrição** caixa de texto.  
  
6. Você pode ocultar ou un-ocultar a pasta, marcando ou desmarcando as **Ocultar este item** caixa de seleção, respectivamente.  
  
7. Selecione **aplicar** para salvar as alterações de propriedades.  
  
8. Opcionalmente, você pode mover ou excluir a pasta selecionando o **mova** ou **excluir** botões na parte superior dos **propriedades** página. Consulte a [mover ou excluir um Item (portal da web)](../../reporting-services/report-server/move-or-delete-an-item-report-manager.md) artigo para obter mais informações.  
  
## <a name="see-also"></a>Confira também  
 [Criar, excluir ou modificar uma pasta (portal da Web)](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)   
 [Gerenciamento do conteúdo do servidor de relatório (Modo Nativo SSRS)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)    
  
::: moniker-end