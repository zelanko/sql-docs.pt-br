---
title: Definir a análise rápida | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dcd1dc09-6eaf-440b-9ce6-fef779ff794f
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 94f4fe123cb37e60e175ad39b932e61376e217b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008942"
---
# <a name="set-fast-parse"></a>Definir a análise rápida
  A propriedade de análise rápida deve ser definida para cada coluna da origem ou transformação que use a análise rápida. Para definir a propriedade, use o Editor avançado da fonte Flat File e da transformação de Conversão de Dados.  
  
### <a name="to-set-fast-parse"></a>Para definir a análise rápida  
  
1.  Clique com o botão direito do mouse na fonte Arquivo Simples ou na transformação de Conversão de Dados e clique em **Mostrar Editor Avançado**.  
  
2.  Na caixa de diálogo **Editor Avançado** , clique na guia **Propriedades de Entrada e Saída** .  
  
3.  No painel **Entradas e Saídas** , clique na coluna para a qual você quer ativar a análise rápida.  
  
4.  Na janela Propriedades, expanda o **propriedades personalizadas** nó e defina o `FastParse` propriedade `True`.  
  
5.  Clique em **OK**.  
  
  