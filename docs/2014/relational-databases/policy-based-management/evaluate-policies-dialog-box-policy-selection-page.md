---
title: Caixa de diálogo Avaliar Políticas, página Seleção de Políticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.dmf.runnow.f1
ms.assetid: 20075fbe-0b48-42c8-b747-690f1aa23dcf
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 674524b53822c1723d45f60715169fe68405e0a8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013104"
---
# <a name="evaluate-policies-dialog-box-policy-selection-page"></a>Caixa de diálogo Avaliar Políticas, página Seleção de Políticas
  Use esta caixa de diálogo para avaliar políticas do Gerenciamento Baseado em Políticas. Ao selecionar a página **Resultados da Avaliação** , você pode aplicar políticas aos itens em um conjunto de destino que não esteja em conformidade com as políticas.  
  
## <a name="options"></a>Opções  
 **Origem**  
 Especifica a origem das políticas. Para alterar a origem, clique no botão Procurar (**...**) para abrir a caixa de diálogo **Selecionar Origem** .  
  
 **Arquivos**  
 Digite o caminho de um arquivo que contenha uma política de Gerenciamento Baseado em Políticas ou use o botão Procurar (**...**) para selecionar o arquivo.  
  
 **Servidor**  
 Selecione para conectar-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que contenha a política desejada.  
  
 **Políticas: Política**  
 Clique para abrir a caixa de diálogo da política especificada.  
  
 **Políticas: Categoria**  
 A categoria da política. Essa caixa é somente leitura.  
  
 **Políticas: Faceta**  
 A faceta implementada pela política. Essa caixa é somente leitura.  
  
 **Avaliar**  
 Executa a política no modo de avaliação. Isso gera um relatório de conformidade para o conjunto de destino, mas não reconfigura o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nem impõe conformidade no futuro.  
  
## <a name="possible-errors"></a>Possíveis erros  
  
-   **Nenhum destino encontrado**  
  
     O conjunto de destino pode estar vazio devido a qualquer um destes motivos:  
  
    -   Na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não há nenhum destino do tipo especificado pela política.  
  
    -   A restrição de servidor pode excluir a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém o destino.  
  
    -   Se a política estiver em um objeto de um banco de dados (por exemplo, uma tabela, exibição ou um usuário), o banco de dados não poderá assinar a categoria da política.  
  
    -   O filtro do conjunto de destino pode excluir todos os destinos dessa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   O tipo de servidor de destino é diferente do tipo de servidor no qual a política é avaliada. Por exemplo, no [!INCLUDE[ssDE](../../includes/ssde-md.md)], se você tentar avaliar uma política criada para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], receberá um conjunto de destino vazio.  
  
## <a name="see-also"></a>Consulte também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](administer-servers-by-using-policy-based-management.md)   
 [Caixa de diálogo Avaliar Políticas, página Resultados da Avaliação](evaluate-policies-dialog-box-evaluation-results-page.md)  
  
  