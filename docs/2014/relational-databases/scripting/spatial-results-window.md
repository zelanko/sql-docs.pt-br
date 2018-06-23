---
title: Janela Resultados Espaciais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c2d5a477-6496-4d01-adee-7322ebdfadf3
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 5a98d82babedc2f60804a1948cd510d59e78b9fe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122809"
---
# <a name="spatial-results-window"></a>Janela Resultados Espaciais
  A janela **Resultados espaciais** fornece ferramentas de mapeamento visuais para exibição de dados espaciais. Para exibir resultados espaciais, os resultados da consulta devem incluir uma coluna espacial com dados de geometria ou de geografia.  
  
> [!NOTE]  
>  A janela **Resultados espaciais** estará disponível apenas se os resultados forem retornados para uma grade na janela **Resultados** . Se você especificar que os resultados são retornados como texto, essa janela não estará disponível.  
  
## <a name="options"></a>Opções  
 **Selecionar coluna espacial**  
 Especifique a coluna espacial que você deseja exibir das colunas espaciais dos resultados da consulta. Apenas uma coluna pode ser selecionada por vez.  
  
 **Selecionar coluna de rótulo**  
 Especifique a coluna não espacial das colunas retornadas nos resultados da consulta para rotular os dados espaciais. Apenas uma coluna pode ser selecionada por vez.  
  
 Essa opção não estará disponível quando apenas instâncias de ponto forem retornadas em uma consulta.  
  
 **Selecionar projeção**  
 Exiba dados de geografia em uma de quatro projeções: Cilíndrica equidistante, Mercator, Robinson ou Bonne.  
  
 Essa opção não está disponível para dados de geometria.  
  
 **Zoom**  
 Ajuste a exibição do mapa em uma escala exponencial.  
  
 **Mostrar linhas de grade**  
 Ative ou desative as linhas de grade das coordenadas.  
  
 Para formas de polígono, o rótulo é exibido apenas quando a forma for grande o suficiente para manter o texto do rótulo. Para exibir rótulos para formas pequenas, ajuste o zoom.  
  
> [!NOTE]  
>  Instâncias de ponto não podem ser rotuladas.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir dados espaciais no Pesquisador de Objetos](view-spatial-data-in-object-explorer.md)   
 [Dados espaciais &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md)   
 [Editor de Consultas do Mecanismo de Banco de Dados &#40;SQL Server Management Studio&#41;](database-engine-query-editor-sql-server-management-studio.md)   
 [Editores de consultas e de texto &#40;SQL Server Management Studio&#41;](query-and-text-editors-sql-server-management-studio.md)  
  
  