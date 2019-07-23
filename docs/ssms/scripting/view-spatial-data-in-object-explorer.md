---
title: Exibir dados espaciais no Pesquisador de Objetos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 59cca562-e3f5-4257-b868-adcbcc0142cc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: facb39a333d148bad2f50c2d87899c308f155168
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68252719"
---
# <a name="view-spatial-data-in-object-explorer"></a>Exibir dados espaciais no Pesquisador de Objetos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  A janela **Resultados espaciais** no Editor de Consultas fornece ferramentas de mapeamento visuais para exibir resultados de dados espaciais além dos dados exibidos em formato de grade na janela **Resultados** . Para exibir dados espaciais na janela **Resultados Espaciais** , os resultados da consulta devem conter pelo menos uma coluna de dados espaciais com dados de geometria ou de geografia.  
  
### <a name="to-view-spatial-data-in-the-spatial-results-window"></a>Para exibir dados espaciais na janela Resultados espaciais  
  
1.  No Editor de Consultas, clique na guia **Resultados espaciais** .  
  
    > [!NOTE]  
    >  Essa janela não estará disponível se os resultados da consulta não contiverem dados espaciais ou se você especificar que os resultados são retornados como texto.  
  
2.  Selecione a coluna que você deseja exibir na lista **Selecionar coluna espacial** . Se houver apenas uma coluna espacial na tabela, essa coluna será a opção padrão na lista.  
  
3.  Selecione a coluna não espacial que você deseja usar como rótulos de dados na lista **Selecionar colunas de rótulos** .  
  
4.  Selecione a projeção desejada para obter dados de geografia na lista **Selecionar projeção** . A projeção padrão é Cilíndrica equidistante. Outras projeções disponíveis são Mercator, Robinson ou Bonne.  
  
    > [!NOTE]  
    >  **Selecionar projeção** não estará disponível se a coluna espacial contiver dados geométricos.  
  
5.  Ajuste o controle deslizante **Zoom** para aumentar o tamanho visual dos elementos mapeados. Para formas de polígono, o rótulo é visível apenas quando a forma for grande o suficiente para manter o texto do rótulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Janela Resultados Espaciais](../../relational-databases/scripting/spatial-results-window.md)   
 [Editor de Consultas do Mecanismo de Banco de Dados &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)   
 [Editores de consultas e de texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)  
  
  
