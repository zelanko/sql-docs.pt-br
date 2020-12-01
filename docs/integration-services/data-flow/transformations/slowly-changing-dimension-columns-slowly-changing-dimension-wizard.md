---
description: Colunas da Dimensão de Alteração Lenta (Assistente para Dimensões de Alteração Lenta)
title: Colunas da Dimensão de Alteração Lenta (Assistente para Dimensões de Alteração Lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8b27c9c0e575775449d2f3a25c5a20bd6667b5cd
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88425718"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>Colunas da Dimensão de Alteração Lenta (Assistente para Dimensões de Alteração Lenta)

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a caixa de diálogo **Colunas de Dimensão de Alteração Lenta** para selecionar um tipo de alteração para cada coluna de dimensão de alteração lenta.  
  
 Para obter mais informações sobre este assistente, consulte [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opções  
 **Colunas de Dimensão**  
 Selecione uma coluna de dimensão na lista.  
  
 **Alterar Tipo**  
 Selecione um **Atributo Fixo** ou um dos dois tipos de atributos de alteração. Use **Atributo Fixo** caso o valor em uma coluna não deva ser alterado; assim o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tratará as alterações como erros. Use **Atributo de alteração** para substituir os valores existentes por com valores alterados. Use **Atributo Histórico** para salvar valores alterados em novos registros, marcando os registros anteriores como desatualizados.  
  
 **Remover**  
 Selecione uma coluna de dimensão e a remova da lista de colunas mapeadas clicando em **Remover**.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar saídas por meio do Assistente para Dimensões de Alteração Lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
