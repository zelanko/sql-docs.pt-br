---
title: Resultados de opções de consulta (página grade) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.grid.f1
ms.assetid: 764bf435-3aab-4c62-b4e0-64fe020a5a95
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7c50957f59ef4e4743ca1667d6eb7a97869bec18
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089012"
---
# <a name="query-options-results-grid-page"></a>Resultados das opções de consultas (Página Grade)
  Use esta página para especificar as opções de exibição de um conjunto de resultados da consulta em formato de grade.  
  
## <a name="options"></a>Opções  
 **Incluir a consulta no conjunto de resultados**  
 Retorna o texto da consulta como parte do conjunto de resultados.  
  
 **Inclua cabeçalhos de coluna ao copiar ou salvar resultados**  
 Inclui os cabeçalhos de coluna (títulos) quando os resultados são copiados para a área de transferência ou quando são salvos em um arquivo. Desmarque essa caixa de seleção se você não deseja que os dados de resultados copiados ou salvos contenham apenas os dados e não os cabeçalhos da coluna.  
  
 **Descartar resultados após a execução**  
 Libera memória descartando os resultados da consulta após a tela tê-los recebido.  
  
 **Exibir resultados em uma guia separada**  
 Exibe o conjunto de resultados em uma janela de documentos nova, em vez de na parte inferior da janela de documentos de consulta.  
  
 **Alternar para a guia Resultados após a execução da consulta**  
 Define automaticamente o foco da tela para o conjunto de resultados.  
  
 **Máximo de Caracteres Recuperados**  
 **Dados não XML**:  
  
 Digite um número de 1 a 65535 para especificar o número máximo de caracteres que serão exibidos em cada célula.  
  
> [!NOTE]  
>  Especificar um número grande de caracteres pode fazer com que os dados no conjunto de resultados apareçam truncados. O número máximo de caracteres exibido em cada célula depende do tamanho da fonte. Quando grandes conjuntos de resultados são retornados, um valor alto nessa caixa pode fazer com que o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] fique com pouca memória e atrapalhe o desempenho do sistema.  
  
 **Dados XML**:  
  
 Selecione **1 MB**, **2 MB**ou **5 MB**. Selecione **Ilimitado** para recuperar todos os caracteres.  
  
 **Restaurar Padrões**  
 Redefine todos os valores dessa página com os valores padrão originais.  
  
  
