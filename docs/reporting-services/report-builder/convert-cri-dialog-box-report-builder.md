---
title: Caixa de diálogo Converter CRI (Construtor de Relatórios) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-builder
ms.topic: reference
f1_keywords:
- "10008"
helpviewer_keywords:
- CRI
- custom report items
ms.assetid: 2a3f2ac6-667e-4498-8b73-9c40beb993f5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e0e1b099d3bd92d5dad8d96f4911585c28f54caa
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294344"
---
# <a name="convert-cri-dialog-box-report-builder"></a>Caixa de diálogo Converter CRI (Construtor de Relatórios)

  Este relatório contém CRIs (itens de relatório personalizados) com recursos sem suporte. CRIs são extensões para a linguagem RDL (Report Definition Language) que oferecem suporte a objetos personalizados que exibem dados em um relatório. Os CRIs incluem componentes em tempo de design e em tempo de execução oferecidos por fornecedores de software de terceiros.  
  
> [!NOTE]  
>  Optar por oferecer suporte a itens de relatório personalizados em um servidor de relatório é uma decisão tomada pelo administrador do sistema. Para exibir CRIs em um relatório, os componentes do CRI devem ser instalados no cliente de criação do relatório para visualizar um relatório e no servidor de relatório para exibir um relatório publicado ou carregado.  
  
 Alguns CRIs podem ser convertidos em itens de relatório no novo formato de definição do relatório. Quando você abre o relatório, precisa confirmar se deseja atualizar. Use as seguintes informações para decidir se você deve converter os CRIs nesse relatório:  
  
-   **Sim** Escolha **Sim** para converter todos os CRIs do relatório, quando possível. Recursos para os quais não há suporte nos CRIs não podem ser atualizados, sendo removidos do arquivo de definição do relatório. Para obter a lista dos recursos sem suporte, consulte [Atualizar relatórios](../../reporting-services/install-windows/upgrade-reports.md). Ao exibir o relatório, você pode ver as diferenças na forma como o CRI é exibido no relatório.  
  
-   **Não** Escolha **Não** quando não quiser converter os CRIs do relatório. Esses CRIs não podem ser exibidos pelo processador de relatório na versão atual. Caso o administrador do sistema pretenda instalar uma nova versão da CRI do fornecedor de software de terceiros compatível com o novo formato de definição do relatório, escolha **Não**. Até que as novas versões estejam disponíveis, os CRIs são exibidos no relatório como uma caixa de texto vazia com um X vermelho.  
  
 Em ambos os casos, o relatório é atualizado para o novo formato de definição de relatório e uma cópia de backup do relatório original é salva como *\<Report Name>* `-` Backup.rdl. Caso salve o relatório na ferramenta de criação do relatório, você está salvando o relatório atualizado no novo formato de definição do relatório. Caso você publique o relatório, ele é salvo primeiro no computador e, em seguida, publicado no servidor de relatório. Você está publicando a versão atualizada do relatório no servidor de relatório.  
  
 Caso você não salve o relatório, o relatório original permanece inalterado. No entanto, não é possível editá-lo em uma versão [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] posterior do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou em um ambiente de criação do relatório que usa este formato de definição do relatório. É possível continuar executando a versão original do relatório carregando-o em um servidor de relatório do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou de versão posterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando o Gerenciador de Relatórios. Para obter mais informações, consulte [Carregar um arquivo ou relatório &#40;Gerenciador de Relatórios&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md).  
  
 Para relatórios carregados, e não publicados em um servidor de relatório, o processador de relatórios determina se o relatório pode ser atualizado no primeiro uso. Os relatórios que não podem ser atualizados são processados no modo de compatibilidade com versões anteriores e continuam a ser exibidos como ocorria na versão anterior do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter mais informações, consulte [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
 Para identificar o formato de definição do relatório atual de um relatório, de um servidor de relatório ou do ambiente de criação do relatório, consulte [Localizar a versão do esquema de definição de relatório &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  

  
  
