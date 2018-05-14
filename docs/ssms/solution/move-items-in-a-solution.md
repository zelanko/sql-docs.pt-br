---
title: Mover itens em uma solução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-solutions
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2c803d45b83e7fdacd51ecf43019b0877d68bea5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="move-items-in-a-solution"></a>Mover itens em uma solução
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Os itens de projeto do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] são consultas, conexões e arquivos diversos. Você pode mover as consultas e os arquivos diversos entre projetos no Gerenciador de Soluções, mas as conexões não podem ser movidas.  
  
### <a name="to-move-items-in-solution-explorer"></a>Para mover itens no Gerenciador de Soluções  
  
1.  No Gerenciador de Soluções, selecione o item que você deseja mover.  
  
2.  No menu **Editar** , clique em **Recortar**.  
  
3.  No Gerenciador de Soluções, selecione o destino.  
  
4.  No menu **Editar** , clique em **Colar**.  
  
Você pode mover itens arrastando consultas e arquivos diversos dentro do Gerenciador de Soluções. Arrastar permite que você veja o resultado da operação. Mover consultas de um tipo de projeto para outro pode fazer com que elas sejam consideradas como arquivos diversos no projeto de destino.  
  
> [!NOTE]  
> Mover uma consulta conectada não move a conexão para o projeto de destino. A consulta perderá sua conexão depois de ser movida para o projeto de destino.  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciador de Soluções](../../ssms/solution/solution-explorer.md)  
[Copiar itens em uma solução](../../ssms/solution/copy-items-in-a-solution.md)  
  
