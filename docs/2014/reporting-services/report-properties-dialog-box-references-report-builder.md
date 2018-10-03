---
title: Relatório de caixa de diálogo de propriedades de referências (construtor de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10082"
ms.assetid: 3414c857-8ea6-4fc4-a6d5-b4883c039efa
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6222a5bfb1efe52e2b35345e7bd6364676936b2b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104576"
---
# <a name="report-properties-dialog-box-references-report-builder"></a>Caixa de diálogo Propriedades do Relatório, Referências (Construtor de Relatórios)
  Selecione **Referências** na caixa de diálogo **Propriedades do Relatório** para adicionar ou remover as referências para assemblies personalizados ou outros assemblies externos e instâncias de classe personalizada usadas pelas expressões na definição do relatório. Assemblies personalizados não têm suporte no modo local no Construtor de Relatórios. Para criar relatórios que usem assemblies personalizados, use o Designer de relatórios no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
## <a name="options"></a>Opções  
 **Adicionar ou remover assemblies**  
 Lista os assemblies aos quais o relatório faz referência. O assembly deve estar disponível no computador no qual a ferramenta que você usando para criar o relatório está instalada e no servidor de relatório. O nome da referência deve corresponder o conteúdo do  **\<CodeModule >** exatamente de marcas no arquivo de linguagem de definição de relatório (. RDL).  
  
 **Adicionar**  
 Clique para adicionar um assembly. Clique no botão de reticências (…) para abrir a caixa de diálogo **Abrir** e selecione os assemblies necessários para concluir o processamento de relatório e a avaliação da expressão.  
  
 **Remover**  
 Para remover uma referência de assembly da lista, selecione o nome do assembly e clique no botão **Remover** .  
  
 **Adicionar ou remover classes**  
 Lista as instâncias de classe usadas pelo relatório. A lista de classe só é usada por membros baseados em instância, não membros estáticos.  
  
 **Adicionar**  
 Clique para adicionar uma referência de classe. Clique no botão de reticências (…) para abrir a caixa de diálogo **Abrir** e selecione as classes necessárias para concluir o processamento de relatório e a avaliação da expressão.  
  
 **Remover**  
 Para excluir a instância de classe, selecione-a e clique no botão **Remover** .  
  
 **Para cima**  
 Para classes que têm dependências, você pode mover esta referência mais para cima na lista.  
  
 **Para baixo**  
 Para classes que têm dependências, você pode mover esta referência mais para baixo na lista.  
  
## <a name="see-also"></a>Consulte também  
 [Ajuda do Construtor de Relatórios para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
  
