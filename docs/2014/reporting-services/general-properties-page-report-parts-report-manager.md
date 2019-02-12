---
title: Página Propriedades gerais, relatórios partes (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 93ddce72-31f1-42f7-abd5-8191acbb00c5
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a3872636fdfda37165bdf6cb83aa13aa51b230b2
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040477"
---
# <a name="general-properties-page-report-parts-report-manager"></a>Página Propriedades Gerais, Partes do Relatório (Gerenciador de Relatórios)
  Use a página Propriedades para exibir e gerenciar as propriedades gerais de uma parte de relatório.  
  
 No Gerenciador de Relatórios, você não pode exibir nem alterar a aparência e a funcionalidade da parte do relatório. Para alterar o design, use uma ferramenta de criação para abrir e modificar o design e publicá-lo novamente no servidor.  
  
## <a name="navigation"></a>Navegação  
 Use o procedimento a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-properties-page-for-a-report-part"></a>Para abrir a página de propriedades de uma parte de relatório  
  
1.  Abra o Gerenciador de Relatórios e localize a parte do relatório cujas propriedades você deseja configurar.  
  
2.  Passe o mouse sobre a parte do relatório e clique na seta do menu suspenso.  
  
3.  Na lista suspensa, clique em **Gerenciar**. A página Propriedades Gerais será aberta.  
  
## <a name="options"></a>Opções  
 **Data da modificação**  
 Data e hora em que as propriedades de parte do relatório foram modificadas pela última vez no servidor ou em que uma nova versão de parte do relatório foi publicada no servidor. Somente leitura.  
  
 **Modificado por**  
 O nome do usuário que modificou por último a parte do relatório. Somente leitura.  
  
 **Data de criação**  
 Data e hora em que parte do relatório foi originalmente publicado no servidor. Somente leitura.  
  
 **Criado por**  
 O nome do usuário que originalmente criou parte do relatório. Somente leitura.  
  
 **Tamanho**  
 O tamanho do arquivo de parte do relatório. Somente leitura.  
  
 **Nome**  
 Digite um nome para identificar a parte de relatório.  
  
 **Descrição**  
 Forneça informações sobre a parte do relatório. A descrição é exibida na página Conteúdo do Gerenciador de Relatórios. O texto da descrição pode ser pesquisado quando um usuário está procurando partes do relatório com uma ferramenta de criação de relatório.  
  
 **Ocultar na exibição de lista**  
 Selecione para ocultar a parte do relatório de usuários que estão usando o modo de exibição de lista no Gerenciador de Relatórios. O modo de exibição de lista é o formato de exibição padrão quando você navega na hierarquia de pastas do servidor de relatório. Embora seja possível ocultar um item na exibição de lista, você não pode ocultá-lo na exibição de detalhes. Se quiser restringir o acesso a um item, você precisará criar uma atribuição de função.  
  
 **Tipo**  
 O tipo de parte do relatório. Somente leitura.  
  
 **Aplicar**  
 Salve as alterações.  
  
 **Delete (excluir)**  
 Remova a parte do relatório do banco de dados do servidor de relatório. A exclusão de parte do relatório do servidor não impedirá a renderização de relatórios existentes aos quais a parte do relatório foi adicionada.  
  
 **Migrar**  
 Clique para abrir a página Mover Itens para mover uma parte do relatório dentro da hierarquia de pastas de servidor de relatório. Para obter mais informações, consulte [página Mover itens &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Download**  
 Extraia uma cópia da definição de parte do relatório a ser salva como um arquivo .rsc. O arquivo .rsc pode ser carregado em uma pasta do servidor de relatório ou usado para substituir uma parte de relatório existente em uma pasta do servidor de relatório.  
  
 **Substituir**  
 Substitua a definição da parte do relatório por outra definição encontrada em um arquivo .rsc.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando partes de relatório](report-design/managing-report-parts.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Partes de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-parts-report-builder-and-ssrs.md)   
 [Ajuda de F1 do Gerenciador de relatórios](../../2014/reporting-services/report-manager-f1-help.md)   
 [Partes de relatório e conjuntos de dados no Construtor de Relatórios](report-data/report-parts-and-datasets-in-report-builder.md)  
  
  
