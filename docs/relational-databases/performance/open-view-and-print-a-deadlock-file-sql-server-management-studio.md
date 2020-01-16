---
title: Abrir, exibir e imprimir um arquivo de deadlock (SSMS)
ms.custom: seo-dt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- deadlocks [SQL Server], printing files
- deadlocks [SQL Server], opening files
- opening deadlock files
- printing deadlock files
ms.assetid: 5061b13f-2cb7-457a-b8d0-fbd437b510ab
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c305d9fd08ffcdd1c4b66d90d834c8f0fb6dead5
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165762"
---
# <a name="open-view-and-print-a-deadlock-file-in-sql-server-management-studio-ssms"></a>Abrir, exibir e imprimir um arquivo de deadlock no SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Quando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] gera um deadlock, é possível capturar e salvar as informações de deadlock em um arquivo. Após salvar o arquivo de deadlock, você pode abri-lo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para exibição ou impressão.  
  
## <a name="open-and-view-a-deadlock-file"></a>Abrir e exibir um arquivo de deadlock  
  
1. No menu **Arquivo** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], aponte para **Abrir** e selecione **Arquivo**.  
  
2. Na caixa de diálogo **Abrir Arquivo** , selecione o tipo de arquivo .xdl na caixa **Arquivos do tipo** . Agora você tem uma lista filtrada, contendo apenas arquivos de deadlock.  
  
## <a name="print-a-deadlock-file"></a>Imprimir um arquivo de deadlock  
  
1. No menu **Arquivo** do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], aponte para **Abrir** e selecione **Arquivo**.  
  
2. Na caixa de diálogo **Abrir Arquivo** , selecione o tipo de arquivo .xdl na caixa **Arquivos do tipo** . Agora você tem uma lista filtrada, contendo apenas arquivos de deadlock.  
  
3. Selecione o arquivo de deadlock que deseja imprimir e selecione **Abrir**.  
  
4. No menu **Arquivo**, selecione **Imprimir**.  
  
## <a name="see-also"></a>Confira também  
 [Salvar gráficos de deadlock &#40;SQL Server Profiler&#41;](../../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md)  
  
  
