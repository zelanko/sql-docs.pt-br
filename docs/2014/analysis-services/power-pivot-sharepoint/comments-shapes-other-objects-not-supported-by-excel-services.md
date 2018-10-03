---
title: 'Os recursos a seguir não têm suporte pelos serviços do Excel e podem não ser exibidos ou ser exibidos apenas parcialmente: comentários, formas ou outros objetos | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: ade92e15-dfbf-496b-9378-a00bd83ba750
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 16269f5c0d7b3d64c9639862995dee44146efb9e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188696"
---
# <a name="the-following-features-are-not-supported-by-excel-services-and-may-not-display-or-may-display-only-partially-comments-shapes-or-other-objects"></a>Os recursos a seguir não têm suporte dos Serviços do Excel e podem não ser exibidos ou ser exibidos apenas parcialmente: Comentários, Formas ou outros objetos
  Este erro ocorre quando você adiciona segmentações de dados a uma pasta de trabalho PowerPivot a partir de uma lista de campos do PowerPivot.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Aplica-se a|PowerPivot para SharePoint|  
|Versão do Produto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|O Excel Web Access não pode renderizar o objeto Forma usado para controlar o posicionamento e a formatação de Segmentações de Dados acrescentadas a uma pasta de trabalho da Lista de Campos do PowerPivot.|  
|Texto da mensagem|Os recursos a seguir não têm suporte dos Serviços do Excel e podem não ser exibidos ou ser exibidos apenas parcialmente:<br /><br /> Comentários, Formas ou outros objetos<br /><br /> Alguns recursos, como consultas de dados externas, exibem dados armazenados em cache que só podem ser atualizados no Microsoft Excel.|  
  
## <a name="explanation"></a>Explicação  
 O Excel Web Access mostra este erro quando você abre uma pasta de trabalho PowerPivot em um navegador e clicar o **detalhes** botão para a mensagem **recursos sem suporte esta pasta de trabalho pode não ser exibidos conforme o esperado**.  
  
 Este erro ocorre porque a pasta de trabalho PowerPivot contém Segmentações de Dados cujo layout é controlado por um objeto Forma oculto no Excel. O objeto Forma controla a formatação e o posicionamento das Segmentações de Dados em posicionamentos horizontais e verticais.  
  
 Os Serviços do Excel não podem renderizar um objeto Forma, mas, como o objeto é oculto, o fato de ele não renderizar não é um problema.  
  
## <a name="user-action"></a>Ação do usuário  
 Este erro pode ser ignorado. Clique em **OK** para fechar a mensagem de erro e continuar a usar a pasta de trabalho e as Segmentações de Dados sem problema.  
  
  
