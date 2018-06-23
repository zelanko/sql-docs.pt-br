---
title: Editor de origem CDC (página colunas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.designer.cdcsource.columns.f1
ms.assetid: bcf3030e-98d8-4445-967c-33c3f8ecb4fc
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 87d5d9b1096e2068759a2100b4daf504849fba0e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013152"
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
 [Editor de origem CDC &#40;página Gerenciador de Conexão&#41;](../../2014/integration-services/cdc-source-editor-connection-manager-page.md)   
 [Editor de origem CDC &#40;página de saída de erro&#41;](../../2014/integration-services/cdc-source-editor-error-output-page.md)  
  
  