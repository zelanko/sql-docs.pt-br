---
title: 'Opções (página XML:Tabs: Editor de texto) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Tabs
ms.assetid: 13bf5f8c-aba3-4c05-b8bb-eb475797c9bd
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: ae595b42274e012032e79754650b573b5d80053b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66089127"
---
# <a name="options-text-editorxmltabs-page"></a>Opções (página Editor de Texto/XML/Guias)
  Essa caixa de diálogo permite alterar o comportamento de tabulação do Editor de XML, que é usado para editar documentos XML. Para exibir essas configurações, clique em **Opções** no menu **Ferramentas** , expanda a pasta **Editor de Texto** , expanda a subpasta **XML** e, então, clique em **Tabulações**.  
  
## <a name="setting-options-in-multiple-locations"></a>Definindo as opções em vários locais  
 As opções do Editor de XML também podem ser definidas na caixa de diálogo **Todos os Idiomas - Geral** . Ao usar as caixas de diálogo **Todos os Idiomas** para definir diferentes opções para os outros editores do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , como o DMX ou MDX, você deverá redefinir as opções do Editor de XML usando essa caixa de diálogo.  
  
## <a name="indenting"></a>Recuo  
 **Nenhum**  
 Quando essa opção estiver selecionada, a nova linha criada ao se pressionar ENTER não ficará recuada. O cursor é colocado na primeira coluna da nova linha.  
  
 **Bloco**  
 Quando esta opção estiver selecionada, a nova linha criada ao se pressionar ENTER ficará recuada automaticamente com a mesma distância da linha anterior.  
  
 **Smart**  
 Quando essa opção é selecionada, a nova linha criada ao se pressionar ENTER é posicionada de acordo com o contexto. Por exemplo, depois de um colchete de abertura ({), as linhas incluídas são automaticamente recuadas para uma parada de tabulação extra. O colchete de fechamento correspondente (}) é realinhado com seu colchete de abertura.  
  
## <a name="tabs"></a>Tabulações  
 **Tamanho da tabulação**  
 Define a distância em espaços entre paradas de tabulação. O padrão é quatro espaços.  
  
 **Tamanho do recuo**  
 Define o tamanho em espaços de um recuo automático. O padrão é quatro espaços. Caracteres de tabulação, caracteres de espaço ou ambos são inseridos para preencher o tamanho especificado.  
  
 **Inserir espaços**  
 Quando essa opção é selecionada, as operações de recuo inserem apenas caracteres de espaço, não caracteres de tabulação. Se **Tamanho do recuo** for definido como 5, por exemplo, cinco caracteres de espaço serão inseridos sempre que a tecla TAB for pressionada ou o botão **Aumentar Recuo** for clicado, na barra de ferramentas na janela principal do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] .  
  
 **Manter tabulações**  
 Quando essa opção é selecionada, as operações de recuo inserem tantos caracteres de tabulação quantos forem possíveis. Cada caractere de tabulação preenche o número de espaços especificado em **Tamanho da tabulação**. Se o **Tamanho do recuo** não for um múltiplo par do **Tamanho da tabulação**, caracteres de espaço serão adicionados para preencher a diferença.  
  
  
