---
title: Mover itens em uma solução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- moving items
- solutions [SQL Server Management Studio], item relocation
- relocating items
ms.assetid: b40a24eb-f528-4e70-b26e-5eaf6e0ed1ed
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 51332c1d9d5076752a3897a12e5e6a1e5a2b6ee2
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65102863"
---
# <a name="move-items-in-a-solution"></a>Mover itens em uma solução
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Os itens de projeto do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] são consultas, conexões e arquivos diversos. Você pode mover as consultas e os arquivos diversos entre projetos no Gerenciador de Soluções, mas as conexões não podem ser movidas.  
  
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
  
