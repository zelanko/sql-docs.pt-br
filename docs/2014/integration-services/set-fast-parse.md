---
title: Definir análise rápida | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: dcd1dc09-6eaf-440b-9ce6-fef779ff794f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7d41b15325586733ab54a37f4c3f007ce0253eaf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055822"
---
# <a name="set-fast-parse"></a>Definir a análise rápida
  A propriedade de análise rápida deve ser definida para cada coluna da origem ou transformação que use a análise rápida. Para definir a propriedade, use o Editor avançado da fonte Flat File e da transformação de Conversão de Dados.  
  
### <a name="to-set-fast-parse"></a>Para definir a análise rápida  
  
1.  Clique com o botão direito do mouse na fonte Arquivo Simples ou na transformação de Conversão de Dados e clique em **Mostrar Editor Avançado**.  
  
2.  Na caixa de diálogo **Editor Avançado** , clique na guia **Propriedades de Entrada e Saída** .  
  
3.  No painel **Entradas e Saídas** , clique na coluna para a qual você quer ativar a análise rápida.  
  
4.  No janela Propriedades, expanda o nó **Propriedades personalizadas** e defina a `FastParse` Propriedade como. `True`  
  
5.  Clique em **OK**.  
  
  
