---
title: Filtrar eventos em um rastreamento
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 0fd63573-3b35-4f67-9e1e-ed9aabee11a8
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 66780fe3a71f784679e80779985740a3d9069777
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75307229"
---
# <a name="filter-events-in-a-trace-sql-server-profiler"></a>Filtrar eventos em um rastreamento (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Os filtros limitam os eventos coletados em um rastreamento. Se não houver um filtro definido, serão retornados todos os eventos das classes de evento selecionadas na saída do rastreamento. Não é obrigatório definir um filtro para um rastreamento. Porém, um filtro minimiza a sobrecarga incorrida durante o rastreamento.  
  
 Os filtros são adicionados às definições de rastreamento por meio da guia **Seleção de Eventos** da caixa de diálogo **Propriedades do Rastreamento** ou **Propriedades do Modelo de Rastreamento** .  
  
### <a name="to-filter-events-in-a-trace"></a>Para filtrar eventos em um rastreamento  
  
1.  Na caixa de diálogo **Propriedades do Rastreamento** ou **Propriedades do Modelo de Rastreamento** , clique na guia **Seleção de Eventos** .  
  
     A guia **Seleção de Eventos** contém um controle de grade. O controle de grade é uma tabela que contém cada uma das classes de evento rastreáveis. A tabela contém uma linha para cada classe de evento. As classes de evento podem diferir ligeiramente, dependendo do tipo e versão de servidor com o qual você está conectado. As classes de evento são identificadas na coluna **Eventos** da grade e são agrupadas por categoria de evento. As colunas restantes listam as colunas de dados que podem ser retornadas para cada classe de evento.  
  
2.  Clique em **Filtros de Coluna.**  
  
     A caixa de diálogo **Editar Filtro** é exibida. A caixa de diálogo **Editar Filtro** contém uma lista de operadores de comparação que podem ser usados para filtrar eventos em um rastreamento.  
  
3.  Para aplicar um filtro, clique no operador de comparação e digite um valor a usar para o filtro.  
  
4.  Clique em **OK**.  
  
 **Considerações:**  
  
-   Se definir condições de filtro nas colunas de dados **StartTime** e **EndTime** da guia Seleção de Eventos, verifique se:  
  
    -   A data inserida corresponda a este formato: `YYYY/MM/DD HH:mm:sec`.  
  
         -OU-  
  
    -   **Usar configurações regionais para exibir valores de data e hora** está marcado na caixa de diálogo **Opções Gerais** . Para exibir a caixa de diálogo **Opções Gerais**, no menu [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] **Ferramentas**, clique em **Opção**.  
  
         -E-  
  
    -   A data inserida esteja entre 1° de janeiro de 1753 e 31 de dezembro de 9999.  
  
-   Se rastrear eventos do utilitário **osql** ou do utilitário **sqlcmd** , sempre acrescente **%** aos filtros na coluna de dados **TextData** .  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
