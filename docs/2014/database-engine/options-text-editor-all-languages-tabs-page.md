---
title: Opções (Editor de texto - todos os idiomas-guias de página) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.All_Languages.Tabs
ms.assetid: bd715d6b-f873-41d4-aa10-57b7098b61cc
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f3e0df6dced5c69f60cbb95abcb5ba8eee78879b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117235"
---
# <a name="options-text-editor---all-languages--tabs-page"></a>Opções (Editor de texto - todos os idiomas-guias de página)
  Use esta caixa de diálogo para definir o comportamento de tabulação nos cinco editores no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Para exibir essas opções, clique em **Opções** no menu **Ferramentas** . Selecione a pasta **Editor de Texto** , expanda a pasta **Todos os Idiomas** e clique em **Tabulações**.  
  
## <a name="tabbing-options-by-editor"></a>Opções de tabulação pelo editor  
 Use a caixa de diálogo **Todos os Idiomas** para definir opções para os editores DMX, MDX e SQL Server Compact. As opções definidas aqui também são aplicadas aos editores de Texto sem formatação, de Transact-SQL e de XML, mas você pode definir opções separadamente para esses editores, expandindo as subpastas para esses idiomas e selecionando as respectivas páginas de opção. Alguns idiomas não dão suporte a todas as opções de tabulação.  
  
> [!CAUTION]  
>  Se você definir uma opção que use essa caixa de diálogo, mas desejar uma configuração diferente para o editor de Texto sem formatação, de Transact-SQL ou de XML, defina as opções para esses editores depois de aplicar suas seleções na caixa de diálogo **Todos os Idiomas** .  
  
 A mensagem "As configurações de recuo (ou guia) para formatos de texto individuais estão em conflito entre si" é exibida quando configurações diferentes são selecionadas para editores específicos. Por exemplo, esse lembrete é exibido se a opção **Recuo do bloco** estiver selecionada para **Texto Sem-Formatação**, mas **Nenhum** estiver selecionada para **XML**.  
  
## <a name="indenting"></a>Recuo  
 **Nenhuma**  
 Quando essa opção estiver selecionada, a nova linha criada ao se pressionar ENTER não ficará recuada. O cursor é colocado na primeira coluna da nova linha.  
  
 **bloco**  
 Quando essa opção é selecionada, a nova linha criada ao se pressionar ENTER é recuada automaticamente com a mesma distância em que a linha anterior foi recuada.  
  
 **Inteligente**  
 Quando essa opção é selecionada, a nova linha criada ao se pressionar ENTER é posicionada de acordo com o contexto.  
  
## <a name="tabs"></a>Tabulações  
 **Tamanho da tabulação**  
 Define a distância em espaços entre paradas de tabulação. O padrão é quatro espaços.  
  
 **Tamanho do recuo**  
 Define o tamanho em espaços de um recuo automático. O padrão é quatro espaços. Caracteres de tabulação, caracteres de espaço ou ambos serão inseridos para preencher o tamanho especificado.  
  
 **Inserir espaços**  
 Quando essa opção é selecionada, as operações de recuo inserem apenas caracteres de espaço, não caracteres de tabulação. Se o **Tamanho do recuo** for definido para 5, por exemplo, então cinco caracteres de espaço são inseridos sempre que se pressionar a tecla TAB ou se clicar no botão **Aumentar Recuo** na barra de ferramentas da janela principal do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] .  
  
 **Manter tabulações**  
 Quando essa opção é selecionada, as operações de recuo inserem tantos caracteres de tabulação quantos forem possíveis. Cada caractere de tabulação preenche o número de espaços especificado em **Tamanho da tabulação**. Se o **Tamanho do recuo** não for um múltiplo par do **Tamanho da tabulação**, caracteres de espaço serão adicionados para preencher a diferença.  
  
  