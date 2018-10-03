---
title: Página de propriedades gerais, pastas (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 31d99d9b-2303-4bae-9466-fb67b97cf11a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f8fca88baa1a3886f06e0c812164d0c759e7d835
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156446"
---
# <a name="general-properties-page-folders-report-manager"></a>Página Propriedades Gerais, Pastas (Gerenciador de Relatórios)
  Use a página Propriedades Gerais de pastas para exibir e definir propriedades para pastas criadas. As informações sobre quem criou ou modificou a pasta e quando ela foi modificada aparecem na parte superior da página Propriedades gerais.  
  
 As propriedades da pasta também incluem configurações de segurança. Para obter mais informações sobre segurança de pasta, consulte [proteger pastas](security/secure-folders.md).  
  
 Pastas de finalidades especiais como Base, Meus Relatórios e pastas de usuários não podem ser renomeadas nem movidas dentro do namespace do servidor de relatório. A página Propriedades Gerais não está disponível para essas pastas.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-general-properties-page-for-a-folder"></a>Para abrir a página Propriedades gerais de uma pasta  
  
1.  Abra o Gerenciador de Relatórios e abra a pasta cujas propriedades você deseja exibir ou configurar.  
  
2.  Sob a faixa da pasta, na barra de ferramentas, clique em **Configurações de Pasta**.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Especifique um nome para a pasta. Um nome deve conter pelo menos um caractere alfanumérico. Também pode conter espaços e alguns símbolos. Não use os caracteres ; ? : \@ & = +, $ * \< > | "ou / ao especificar um nome.  
  
 **Descrição**  
 Digite uma descrição dos conteúdos de pasta. Essa descrição aparece na página Conteúdo para usuários com permissão para acessar a pasta.  
  
 **Ocultar na exibição de lista**  
 Selecione essa opção para ocultar a pasta de usuários que estão usando modo de exibição de lista no Gerenciador de Relatórios. O modo de exibição de lista é o formato de exibição padrão quando se navega na hierarquia de pastas do servidor de relatórios. Na exibição de lista, os nomes de itens e as descrições fluem pela página. O formato alternativo é o modo de exibição de detalhes. A exibição de detalhes omite descrições, mas contém outras informações sobre o item. Embora seja possível ocultar um item na exibição de lista, você não pode ocultá-lo na exibição de detalhes. Se quiser restringir o acesso a um item, você precisará criar uma atribuição de função.  
  
 **Aplicar**  
 Clique para salvar as alterações.  
  
 **Delete (excluir)**  
 Clique para remover a pasta e seus conteúdos.  
  
 **Migrar**  
 Clique para realocar um relatório ou pasta dentro do namespace do servidor de relatório. Clicar nesse botão abre a página Mover Itens, que lhe permite navegar pelas pastas para um novo local de pasta.  
  
## <a name="see-also"></a>Consulte também  
 [O Gerenciador de relatórios &#40;modo nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
