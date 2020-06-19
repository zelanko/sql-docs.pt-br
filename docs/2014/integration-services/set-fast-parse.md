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
ms.openlocfilehash: bb0fefd2f9c06d6bcff44c211904a951ebe01937
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963346"
---
# <a name="set-fast-parse"></a>Definir a análise rápida
  A propriedade de análise rápida deve ser definida para cada coluna da origem ou transformação que use a análise rápida. Para definir a propriedade, use o Editor avançado da fonte Flat File e da transformação de Conversão de Dados.  
  
### <a name="to-set-fast-parse"></a>Para definir a análise rápida  
  
1.  Clique com o botão direito do mouse na fonte Arquivo Simples ou na transformação de Conversão de Dados e clique em **Mostrar Editor Avançado**.  
  
2.  Na caixa de diálogo **Editor Avançado** , clique na guia **Propriedades de Entrada e Saída** .  
  
3.  No painel **Entradas e Saídas** , clique na coluna para a qual você quer ativar a análise rápida.  
  
4.  No janela Propriedades, expanda o nó **Propriedades personalizadas** e defina a `FastParse` propriedade como `True` .  
  
5.  Clique em **OK**.  
  
  
