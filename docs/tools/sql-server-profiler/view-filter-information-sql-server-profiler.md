---
title: Exibir informações de filtro
titleSuffix: SQL Server Profiler
description: Descubra como exibir os filtros que SQL Server Profiler está aplicando atualmente a colunas de dados para limitar os eventos que são rastreados.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 8d002dea-376a-452c-b3ca-3e93656ed75f
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 786b85d9c2f9707c26a18c3a7ddef27a127090c6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759531"
---
# <a name="view-filter-information-sql-server-profiler"></a>Exibir informações de filtro (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este tópico descreve como exibir filtros em colunas de dados de classes de evento, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="to-view-filter-information"></a>Para exibir informações de filtro  
  
1.  Abra um arquivo de rastreamento, tabela de rastreamento ou um script SQL e, no menu **Arquivo** , clique em **Propriedades**. Se você estiver editando um modelo de rastreamento ou criando um rastreamento novo, ignore esta etapa.  
  
2.  Na guia **Seleção de Eventos** , clique com o botão direito do mouse no nome da coluna de dados do filtro que deseja exibir e clique em **Editar Filtro de Coluna**.  
  
3.  Na caixa de diálogo **Editar Filtro** , expanda os operadores de comparação de filtro para consultar o valor atribuído ao critério especificado. Repita as Etapas 2 e 3 para todas as colunas cujas informações de filtro quiser visualizar.  
  
> [!NOTE]  
>  Operadores de comparação que já têm valores atribuídos são formatados em negrito.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
