---
title: Opções (Editor de texto - o Transact-SQL - guias página) | Microsoft Docs
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
- VS.ToolsOptionsPages.Text_Editor.SQL.Tabs
dev_langs:
- TSQL
ms.assetid: a4499784-67f7-46ef-9f7c-2d0fdd117a52
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c070024769f59516f57d89a4c76b97ceb9b775f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118496"
---
# <a name="options-text-editor---transact-sql---tabs-page"></a>Opções (página do Editor de texto - o Transact-SQL - guias)
  Use esta caixa de diálogo para alterar o comportamento de tabulação do Editor de Consultas [!INCLUDE[ssDE](../includes/ssde-md.md)] , que é usado para programar scripts [!INCLUDE[tsql](../includes/tsql-md.md)] . Para exibir essas configurações, clique em **Opções** no menu **Ferramentas** , expanda a pasta **Editor de Texto** , expanda a subpasta **Transact-SQL** e, em seguida, clique em **Tabulações**.  
  
## <a name="setting-options-in-multiple-locations"></a>Definindo as opções em vários locais  
 As opções do Editor de Consultas [!INCLUDE[ssDE](../includes/ssde-md.md)] também podem ser definidas no diálogo **Todos os Idiomas, Guias** . Ao usar as caixas de diálogo **Todos os Idiomas** para definir diferentes opções para os outros editores do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , como o DMX ou MDX, você deverá redefinir as opções do Editor de Consultas do [!INCLUDE[ssDE](../includes/ssde-md.md)] usando essa caixa de diálogo.  
  
## <a name="indenting"></a>Recuo  
 **Nenhuma**  
 Quando essa opção estiver selecionada, a nova linha criada ao se pressionar ENTER não ficará recuada. O cursor é colocado na primeira coluna da nova linha.  
  
 **bloco**  
 Quando esta opção estiver selecionada, a nova linha criada ao se pressionar ENTER ficará recuada automaticamente com a mesma distância da linha anterior.  
  
 **Inteligente**  
 Esta opção não está disponível.  
  
## <a name="tabs"></a>Tabulações  
 **Tamanho da tabulação**  
 Define a distância em espaços entre paradas de tabulação. O padrão é quatro espaços.  
  
 **Tamanho do recuo**  
 Define o tamanho em espaços de um recuo automático. O padrão é quatro espaços. Caracteres de tabulação, caracteres de espaço ou ambos são inseridos para preencher o tamanho especificado.  
  
 **Inserir espaços**  
 Quando essa opção é selecionada, as operações de recuo inserem apenas caracteres de espaço, não caracteres de tabulação. Se **Tamanho do recuo** for definido como 5, por exemplo, cinco caracteres de espaço serão inseridos sempre que a tecla TAB for pressionada ou o botão **Aumentar Recuo** for clicado, na barra de ferramentas na janela principal do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] .  
  
 **Manter tabulações**  
 Quando essa opção é selecionada, as operações de recuo inserem tantos caracteres de tabulação quantos forem possíveis. Cada caractere de tabulação preenche o número de espaços especificado em **Tamanho da tabulação**. Se o **Tamanho do recuo** não for um múltiplo par do **Tamanho da tabulação**, caracteres de espaço serão adicionados para preencher a diferença.  
  
  