---
title: Página de propriedades gerais, modelos (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.general.f1
ms.assetid: 7ad59850-8135-4c4d-95e9-6d705b6d77a8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2523909f2719fb8316acecf8ad0b56ddbe086a36
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63260805"
---
# <a name="general-properties-page-models-report-manager"></a>Página Propriedades Gerais, Modelos (Gerenciador de Relatórios)
  Use a página Propriedades Gerais para que os modelos de relatório renomeiem, movam ou substituam o arquivo de definição do modelo (.smdl). Os detalhes sobre quem criou ou modificou o modelo e quando as alterações ocorreram são indicados na parte superior da página.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-general-properties-page-for-a-model"></a>Para abrir a página de propriedades Geral de um modelo  
  
1.  Abra o Gerenciador de Relatórios e localize o modelo cujas propriedades você deseja exibir ou configurar.  
  
2.  Focalize o modelo e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do modelo.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifica o nome do modelo. Um nome deve conter pelo menos um caractere alfanumérico. Também pode conter espaços e alguns símbolos. Não use os seguintes caracteres ao especificar um nome:  
  
 ; ? : \@ & = + , $ / * \< > | " /  
  
 **Descrição**  
 Digite uma descrição do modelo. Essa descrição é exibida na página Conteúdo para usuários com permissão de acessar o modelo.  
  
 **Oculto na exibição de lista**  
 Marque esta caixa de seleção para ocultar o item quando a pasta for definida na exibição de lista. Exibição de lista é um modo de exibição do conteúdo da pasta que tem o suporte do Gerenciador de Relatórios. Você pode definir essa opção no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para definir como esse item é exibido no Gerenciador de Relatórios. Para obter mais informações sobre modos de exibição no Gerenciador de relatórios, consulte [página de conteúdo &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/contents-page-report-manager.md).  
  
 **Aplicar**  
 Clique para salvar as alterações.  
  
 **Delete (excluir)**  
 Clique para remover o modelo do banco de dados do servidor de relatório. A exclusão de um modelo não exclui a fonte de dados compartilhada dependente que fornece informações de conexão nem exclui relatórios que usam o modelo como uma fonte de dados. Porém, depois que o modelo é excluído, informa que o uso do modelo não será mais executado.  
  
 **Migrar**  
 Clique para realocar um modelo dentro da hierarquia de pasta do servidor de relatório. O clique nesse botão abre a página Mover Itens, na qual você pode navegar até um novo local de pasta. Para obter mais informações, consulte [página Mover itens &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Salvar**  
 Clique para salvar uma cópia somente leitura da definição do modelo. Dependendo das associações de arquivo definidas no computador, o arquivo abrirá no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou em um aplicativo diferente. Na maioria dos casos, o modelo abre como um arquivo XML.  
  
 A cópia que você abre é idêntica à definição do modelo original inicialmente publicada no servidor de relatório. Quaisquer propriedades definidas no modelo após sua publicação (como propriedades de fonte de dados) não serão refletidas no arquivo que você abrir.  
  
 Você pode modificar a definição do modelo e salvá-lo em um novo arquivo em uma pasta compartilhada e carregar a definição do modelo para o servidor de relatório como um novo item. Modificações feitas na definição do modelo enquanto ele está aberto no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (ou outro aplicativo) não são salvas diretamente no servidor de relatório. Você deve carregar o arquivo para publicar o modelo modificado no servidor de relatório.  
  
 Observe que, se você quiser abrir o modelo de relatório no Designer de Modelo, deverá salvar o modelo como um arquivo .smdl e, em seguida, adicionar esse arquivo a um projeto no Designer de Modelo.  
  
 **Substituir**  
 Clique para substituir a definição do modelo por outra de um arquivo .smdl localizado no sistema de arquivos. Se você atualizar uma definição de modelo, deverá redefinir as configurações de fonte de dados compartilhada depois que a atualização for concluída.  
  
 **Regenerar modelo**  
 Clique para regenerar um modelo padrão que substitui a versão atual. Essa opção é exibida depois que o modelo é gerado. O modelo gerado é baseado na fonte de dados compartilhada. Ele não pode ser personalizado antes de ser gerado. Entretanto, depois que ele é gerado, você pode clicar em **Editar** para abrir a definição do modelo, salvá-la no sistema de arquivos e adicioná-la a um projeto no Designer de Modelo. Depois de refinar o modelo, você pode carregá-lo no servidor de relatório como um novo item ou clique em **Atualizar** nessa página para substituir o modelo gerado pela versão revisada no Designer de Modelo.  
  
## <a name="see-also"></a>Consulte também  
 [Associar um relatório ou modelo a uma fonte de dados compartilhada &#40;SSRS&#41;](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](tools/report-server-in-management-studio-f1-help.md)  
  
  
