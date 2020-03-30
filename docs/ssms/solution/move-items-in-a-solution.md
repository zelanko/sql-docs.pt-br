---
title: Mover itens em uma solução
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 256e2ff3dc5b1cde4dd2e5dc5e065f01b073eb33
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75251844"
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
  
