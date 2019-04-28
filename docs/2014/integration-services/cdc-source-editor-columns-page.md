---
title: Editor de origem CDC (página colunas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsource.columns.f1
ms.assetid: bcf3030e-98d8-4445-967c-33c3f8ecb4fc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4f1c9a636023e4dc9c5c9ffb69240921e780ed38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62836160"
---
# <a name="cdc-source-editor-columns-page"></a>Editor de Origem CDC (página Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Origem CDC** para mapear uma coluna de saída em cada coluna externa (origem).  
  
 Para obter mais informações sobre a origem CDC, consulte [CDC Source](data-flow/cdc-source.md).  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página Colunas do Editor de Origem CDC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tem a origem CDC.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na origem CDC.  
  
3.  No **Editor de Origem CDC**, clique em **Colunas**.  
  
## <a name="options"></a>Opções  
 **Colunas Externas Disponíveis**  
 A lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas. Selecione as colunas a serem usadas na origem. As colunas selecionadas são adicionadas à lista **Coluna Externa** na ordem em que são selecionadas.  
  
 **Coluna Externa**  
 Uma exibição das colunas externas (origem) na ordem em que serão exibidas ao configurar os componentes que consomem os dados da origem CDC. Para alterar essa ordem, primeiro limpe as colunas selecionadas na lista **Colunas Externas Disponíveis** e depois selecione colunas externas na lista em uma ordem diferente. As colunas selecionadas são adicionadas à lista **Coluna Externa** na ordem em que são selecionadas.  
  
 **Coluna de Saída**  
 Insira um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome inserido é exibido no Designer SSIS.  
  
## <a name="see-also"></a>Consulte também  
 [Editor de Origem CDC &#40;Página Gerenciador de Conexões&#41;](../../2014/integration-services/cdc-source-editor-connection-manager-page.md)   
 [Editor de Origem CDC &#40;Página Saída de Erro&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  
