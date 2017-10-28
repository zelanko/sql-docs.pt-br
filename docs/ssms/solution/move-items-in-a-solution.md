---
title: "Mover itens em uma solução | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b0140646e92871aa5d3ab2acbb95b417ab38d28b
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="move-items-in-a-solution"></a>Mover itens em uma solução
Os itens de projeto do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] são consultas, conexões e arquivos diversos. Você pode mover as consultas e os arquivos diversos entre projetos no Gerenciador de Soluções, mas as conexões não podem ser movidas.  
  
### <a name="to-move-items-in-solution-explorer"></a>Para mover itens no Gerenciador de Soluções  
  
1.  No Gerenciador de Soluções, selecione o item que você deseja mover.  
  
2.  No menu **Editar** , clique em **Recortar**.  
  
3.  No Gerenciador de Soluções, selecione o destino.  
  
4.  No menu **Editar** , clique em **Colar**.  
  
Você pode mover itens arrastando consultas e arquivos diversos dentro do Gerenciador de Soluções. Arrastar permite que você veja o resultado da operação. Mover consultas de um tipo de projeto para outro pode fazer com que elas sejam consideradas como arquivos diversos no projeto de destino.  
  
> [!NOTE]  
> Mover uma consulta conectada não move a conexão para o projeto de destino. A consulta perderá sua conexão depois de ser movida para o projeto de destino.  
  
## <a name="see-also"></a>Consulte também  
[Gerenciador de Soluções](../../ssms/solution/solution-explorer.md)  
[Copiar itens em uma solução](../../ssms/solution/copy-items-in-a-solution.md)  
  

