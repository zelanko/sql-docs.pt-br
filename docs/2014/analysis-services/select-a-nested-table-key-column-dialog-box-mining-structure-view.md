---
title: Selecione uma caixa de diálogo de coluna de chave de tabela aninhada (exibição de estrutura de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.structure.addnestedtable.f1
helpviewer_keywords:
- Select a Nested Table Key Column dialog box
ms.assetid: f68b89a7-17df-45f8-ba7f-b458cd9b1ec3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7eaccd916ee401ad1b6b82a155e50688b2ff57a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227527"
---
# <a name="select-a-nested-table-key-column-dialog-box-mining-structure-view"></a>Selecione uma caixa de diálogo de coluna de chave de tabela aninhada (exibição de estrutura de mineração)
  Use a caixa de diálogo **Selecionar uma Coluna de Chave de Tabela Aninhada** para designar uma coluna que funcionará como chave da nova tabela aninhada. Quando você sair da caixa de diálogo, uma nova tabela será adicionada para a estrutura de mineração que contém a coluna de chave. Você pode adicionar colunas à tabela aninhada clicando com o botão direito na estrutura e selecionando **Adicionar uma Coluna**. A caixa de diálogo contém diferentes opções dependendo se você esta trabalhando com um modelo de mineração OLAP ou um modelo de mineração relacional.  
  
## <a name="options"></a>Opções  
 **Tabela de origem**  
 A tabela na qual o modelo de mineração esta baseado.  
  
 Isto só é usado para modelos de mineração relacionais.  
  
 **Coluna de origem**  
 Uma lista de todas as colunas disponíveis na tabela de origem que você pode usar como chave da tabela aninhada.  
  
 Isto só é usado para modelos de mineração relacionais.  
  
 **Mostrar tipos de coluna**  
 Uma lista de tipos de dados de coluna disponíveis. Selecione ou desmarque os tipos de dados para filtrar a lista de colunas em **Coluna de origem**. Só serão mostradas colunas que correspondem aos tipos de dados marcados na lista **Coluna de origem** .  
  
 Isto só é usado para modelos de mineração relacionais.  
  
 **Atributos**  
 Uma lista de atributos que você pode usar como a chave da tabela aninhada.  
  
 Isto só é usado para modelos de mineração de OLAP.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de estrutura de mineração &#40;Designer de modelo de mineração de dados&#41;](mining-structure-view-data-mining-model-designer.md)  
  
  
