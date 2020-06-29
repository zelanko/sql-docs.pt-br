---
title: Colunas da Dimensão de Alteração Lenta (Assistente para Dimensões de Alteração Lenta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6283887cbddb9844e0ac769281184f588dc2a94d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85430253"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>Colunas da Dimensão de Alteração Lenta (Assistente para Dimensões de Alteração Lenta)
  Use a caixa de diálogo **Colunas de Dimensão de Alteração Lenta** para selecionar um tipo de alteração para cada coluna de dimensão de alteração lenta.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opções  
 **Colunas de Dimensão**  
 Selecione uma coluna de dimensão na lista.  
  
 **Alterar Tipo**  
 Selecione um **Atributo Fixo**ou um dos dois tipos de atributos de alteração. Use **Atributo Fixo** caso o valor em uma coluna não deva ser alterado; assim o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tratará as alterações como erros. Use **Atributo de alteração** para substituir os valores existentes por com valores alterados. Use **Atributo Histórico** para salvar valores alterados em novos registros, marcando os registros anteriores como desatualizados.  
  
 **Remover**  
 Selecione uma coluna de dimensão e a remova da lista de colunas mapeadas clicando em **Remover**.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
