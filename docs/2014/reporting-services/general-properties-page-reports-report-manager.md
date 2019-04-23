---
title: Página Propriedades gerais, relatórios (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 66c99d28-ab41-45f0-bf02-ed560293595d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c44bc306aaa1e55aa5005663ecfcfbf261576593
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59940283"
---
# <a name="general-properties-page-reports-report-manager"></a>Página Propriedades Gerais, Relatórios (Gerenciador de Relatórios)
  Use a página Propriedades Gerais para que os relatórios renomeiem, excluam, movam ou substituam a definição do relatório. Você também pode usar essa página para criar um relatório vinculado. Detalhes sobre quem criou ou modificou o relatório e quando as alterações ocorreram são indicados na parte superior da página.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-general-properties-page-for-a-report"></a>Para abrir a página Propriedades gerais de um relatório  
  
1.  Abra o Gerenciador de Relatórios e localize o relatório cujas propriedades você deseja exibir ou configurar.  
  
2.  Focalize o relatório e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página de propriedades Geral do relatório.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifique um nome para o relatório. Um nome deve conter pelo menos um caractere alfanumérico. Também pode conter espaços e certos símbolos. Não use os caracteres ; ? : \@ & = + , $ * \< >  
  
 " ou / ao especificar um nome.  
  
 **Descrição**  
 Digite uma descrição do relatório. Essa descrição aparece na página Conteúdo para usuários com permissão para acessar o relatório.  
  
 **Ocultar na exibição de lista**  
 Selecione essa opção para ocultar o relatório de usuários que estão usando modo de exibição de lista no Gerenciador de Relatórios. O modo de exibição de lista é o formato de exibição padrão quando se navega na hierarquia de pastas do servidor de relatórios. Na exibição de lista, os nomes de itens e as descrições fluem pela página. O formato alternativo é o modo de exibição de detalhes. A exibição de detalhes omite descrições, mas contém outras informações sobre o item. Embora seja possível ocultar um item na exibição de lista, você não pode ocultá-lo na exibição de detalhes. Se quiser restringir o acesso a um item, você precisará criar uma atribuição de função.  
  
 **Aplicar**  
 Clique para salvar as alterações.  
  
 **Delete (excluir)**  
 Clique para remover o relatório do banco de dados do servidor de relatório. A exclusão de um relatório exclui todo o histórico de relatório associado e agendas e assinaturas específicas de relatório. Se o relatório for associado com relatórios vinculados, os relatórios vinculados serão invalidados.  
  
 **Migrar**  
 Clique para realocar um relatório na hierarquia de pasta do servidor de relatório. O clique nesse botão abre a página Mover Itens, na qual você pode navegar até um novo local de pasta. Para obter mais informações, consulte [página Mover itens &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Criar relatório vinculado**  
 Clique para abrir a página Novo Relatório Vinculado. Para obter mais informações sobre essa página e relatórios vinculados, consulte [página novo relatório vinculado &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/new-linked-report-page-report-manager.md).  
  
 **Salvar**  
 Clique para extrair uma cópia somente leitura da definição do relatório. Dependendo das associações de arquivo definidas no computador, o arquivo abrirá no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ou em um aplicativo diferente. Na maioria dos casos, o relatório é aberto como um arquivo XML.  
  
 A cópia que você abre é idêntica à definição do relatório original inicialmente publicado no servidor de relatórios. Quaisquer propriedades definidas no relatório após sua publicação (como parâmetros e fonte de dados) não se refletem no arquivo que você abre.  
  
 Você pode modificar a definição do relatório e salvá-lo em um novo arquivo em uma pasta compartilhada e carregar a definição do relatório para o servidor de relatório como um novo item. Modificações feitas na definição do relatório enquanto ele está aberto no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (ou outro aplicativo) não são salvas diretamente no servidor de relatório. Você deve carregar o arquivo para publicar o relatório modificado no servidor de relatório.  
  
 **Substituir**  
 Clique para substituir a definição do relatório usada no relatório atual por uma diferente de um arquivo .rdl localizado no sistema de arquivos. Se você atualizar uma definição do relatório, deve reajustar as configurações de fonte de dados quando a atualização for concluída.  
  
 **Alterar Link**  
 Clique para selecionar uma definição de relatório diferente para o relatório vinculado. Essa opção será exibida se o relatório for um relatório vinculado. Se o relatório for vinculado, você poderá definir essa propriedade para substituir a definição do relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
