---
title: Opções (Editor de texto - texto sem formatação - guias página) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.Tabs
ms.assetid: 07d82d10-bca9-4b37-abbb-58ef9bfb264b
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5c27514ea38602885c26733238f2564211d4f43a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115497"
---
# <a name="options-text-editor---plain-text---tabs-page"></a>Options (Text Editor - Plain Text - Tabs Page)
  Use essa caixa de diálogo para alterar o comportamento de tabulação do Editor de Texto, que é usado para editar um documento não associado a um idioma de desenvolvimento específico. Para exibir essas configurações, clique em **Opções** no menu **Ferramentas** , expanda a pasta **Editor de Texto**, expanda **Texto Sem-formatação**e, então, clique em **Tabulações**.  
  
## <a name="setting-options-in-multiple-locations"></a>Definindo as opções em vários locais  
 As opções do Editor de Texto sem Formatação também podem ser definidas na caixa de diálogo **Todos os Idiomas - Geral** . Ao usar as caixas de diálogo **Todos os Idiomas** para definir diferentes opções para os outros editores do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , como o DMX ou MDX, você deverá redefinir as opções do Editor de Texto sem Formatação usando essa caixa de diálogo.  
  
## <a name="indenting"></a>Recuo  
 **Nenhuma**  
 Não recue a nova linha criada ao pressionar ENTER. O cursor é colocado na primeira coluna da nova linha.  
  
 **bloco**  
 Recue a nova linha criada ao pressionar ENTER com a mesma distância de recuo que a da linha anterior.  
  
 **Inteligente**  
 O editor de texto sem-formatação não oferece suporte para esse tipo de formatação.  
  
## <a name="tabs"></a>Tabulações  
 **Tamanho da tabulação**  
 Defina a distância em espaços entre paradas de tabulação. O padrão é quatro espaços.  
  
 **Tamanho do recuo**  
 Defina o tamanho em espaços de um recuo automático. O padrão é quatro espaços. Caracteres de tabulação, caracteres de espaço ou ambos serão inseridos para preencher o tamanho especificado.  
  
 **Inserir espaços**  
 Ao recuar, insira apenas caracteres de espaço, não caracteres de guia. Se **Tamanho do recuo** for definido em 5, por exemplo, cinco caracteres de espaço são inseridos sempre que se pressionar a tecla TAB ou o botão **Aumentar Recuo** , na barra de ferramentas **Formatação** .  
  
 **Manter tabulações**  
 Ao recuar, insira tantos caracteres de guia quanto possível. Cada caractere de tabulação preenche o número de espaços especificado em **Tamanho da tabulação**. Se o **Tamanho do recuo** não for um múltiplo par do **Tamanho da guia**, caracteres de espaço serão adicionados para preencher a diferença.  
  
  