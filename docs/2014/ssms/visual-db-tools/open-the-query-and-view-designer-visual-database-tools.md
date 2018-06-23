---
title: Abrir no Designer de Consulta e Exibição (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- opening View Designer
- View Designer, opening
- Query Designer [SQL Server], opening
- opening Query Designer
ms.assetid: b473f258-d53c-41c0-9ad9-528a2ff141f4
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: e822f9facf894ccebf4408316d2ed8166ff64d5f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122962"
---
# <a name="open-the-query-and-view-designer-visual-database-tools"></a>Abrir o Designer de Consulta e Exibição (Visual Database Tools)
  O Designer de Consulta e Exibição é aberto quando a definição de uma exibição é aberta; mostra os resultados de uma consulta ou exibição, ou cria ou abre uma consulta. Consiste em quatro painéis separados:  
  
-   O painel Diagrama apresenta uma exibição gráfica das tabelas ou objetos com valor de tabela selecionados na conexão de dados. Mostra também todas as relações de junção entre eles.  
  
-   O painel Critérios permite que sejam especificadas as opções de consulta – tais como colunas de dados a exibir, como ordenar os resultados e quais linhas selecionar – inserindo as seleções em uma grade de planilha.  
  
-   Você pode usar o painel SQL para criar sua própria instrução SQL, ou pode usar os painéis de Critérios e Diagrama para criar a instrução, caso em que as instruções SQL serão criadas no painel SQL. À medida que você cria a consulta, o painel SQL é atualizado e reformatado automaticamente para ser lido com facilidade.  
  
-   O painel Resultados mostra os resultados da consulta Selecionar executada mais recentemente. (Os resultados de outros tipos de consultas são exibidos em caixas de mensagens.)  
  
-   Esses painéis são úteis por trabalharem tanto com consultas quanto com exibições.  
  
-   Quando uma exibição ou consulta é aberta, alguns dos painéis são também abertos. Quais são esses painéis dependerá das configurações da caixa de diálogo **Opções** e do sistema de gerenciamento de banco de dados ao qual você está conectado. O padrão é que todos os quatro sejam abertos.  
  
### <a name="to-open-the-query-and-view-designer-for-a-view"></a>Para brir o Designer de Consulta e Exibição para uma exibição  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na exibição que você deseja abrir e depois clique em **Design** ou **Abrir Exibição**.  
  
     Se você escolher **Design**, o Designer de Consulta e Exibição será aberto na forma determinada pelas opções selecionadas na caixa de diálogo **Opções** . Se você escolher **Abrir Exibição**, apenas o painel de Resultados será aberto por padrão.  
  
### <a name="to-open-the-query-and-view-designer-for-an-existing-query"></a>Para abrir o Designer de Consulta e Exibição para uma consulta existente  
  
1.  No Gerenciador de Soluções, expanda a pasta **Consultas** .  
  
2.  Clique duas vezes na consulta a ser aberta.  
  
3.  Realce as instruções de consulta, clique com o botão direito do mouse na área realçada e depois clique em **Projetar Consulta no Editor**.  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos de instruções de consultas e modos de exibição de design &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Ferramentas do Designer de Consulta e Exibição &#40;Visual Database Tools&#41;](query-and-view-designer-tools-visual-database-tools.md)  
  
  