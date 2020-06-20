---
title: Opções (página Editor de texto – Transact-SQL – guias) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.Tabs
dev_langs:
- TSQL
ms.assetid: a4499784-67f7-46ef-9f7c-2d0fdd117a52
author: rothja
ms.author: jroth
ms.openlocfilehash: 5a713b3c3f98d2510fa63ddd6a58e2f48f3b3495
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929695"
---
# <a name="options-text-editor---transact-sql---tabs-page"></a>Opções (página Editor de texto – Transact-SQL – guias)
  Use esta caixa de diálogo para alterar o comportamento de tabulação do Editor de Consultas [!INCLUDE[ssDE](../includes/ssde-md.md)] , que é usado para programar scripts [!INCLUDE[tsql](../includes/tsql-md.md)] . Para exibir essas configurações, clique em **Opções** no menu **Ferramentas** , expanda a pasta **Editor de Texto** , expanda a subpasta **Transact-SQL** e, em seguida, clique em **Tabulações**.  
  
## <a name="setting-options-in-multiple-locations"></a>Definindo as opções em vários locais  
 As opções do Editor de Consultas [!INCLUDE[ssDE](../includes/ssde-md.md)] também podem ser definidas na caixa de diálogo **Todas as Guias de Idiomas**. Ao usar as caixas de diálogo **Todos os Idiomas** para definir diferentes opções para os outros editores do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] , como o DMX ou MDX, você deverá redefinir as opções do Editor de Consultas do [!INCLUDE[ssDE](../includes/ssde-md.md)] usando essa caixa de diálogo.  
  
## <a name="indenting"></a>Recuo  
 **Nenhuma**  
 Quando essa opção estiver selecionada, a nova linha criada ao se pressionar ENTER não ficará recuada. O cursor é colocado na primeira coluna da nova linha.  
  
 **Bloquear**  
 Quando esta opção estiver selecionada, a nova linha criada ao se pressionar ENTER ficará recuada automaticamente com a mesma distância da linha anterior.  
  
 **Inteligente**  
 Esta opção não está disponível.  
  
## <a name="tabs"></a>Tabulações  
 **Tamanho da tabulação**  
 Define a distância em espaços entre paradas de tabulação. O padrão é quatro espaços.  
  
 **Tamanho do recuo**  
 Define o tamanho em espaços de um recuo automático. O padrão é quatro espaços. Caracteres de tabulação, caracteres de espaço ou ambos são inseridos para preencher o tamanho especificado.  
  
 **Inserir espaços**  
 Quando essa opção é selecionada, as operações de recuo inserem apenas caracteres de espaço, não caracteres de tabulação. Se o **tamanho do recuo** for definido como 5, por exemplo, cinco caracteres de espaço serão inseridos sempre que você pressionar a tecla TAB ou clicar no botão **aumentar recuo** na barra de ferramentas na [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] janela principal.  
  
 **Manter tabulações**  
 Quando essa opção é selecionada, as operações de recuo inserem tantos caracteres de tabulação quantos forem possíveis. Cada caractere de tabulação preenche o número de espaços especificado em **Tamanho da tabulação**. Se o **Tamanho do recuo** não for um múltiplo par do **Tamanho da tabulação**, caracteres de espaço serão adicionados para preencher a diferença.  
  
  
