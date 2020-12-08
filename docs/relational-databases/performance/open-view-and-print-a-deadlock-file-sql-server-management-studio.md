---
title: Abrir, exibir e imprimir um arquivo de deadlock (SSMS)
description: Saiba como capturar as informações sobre deadlocks que o SQL Server Profiler gera e como exibi-las no SQL Server Management Studio.
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
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c5d778526336ce26a4cfb7932971a1be275a5dda
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505110"
---
# <a name="open-view-and-print-a-deadlock-file-in-sql-server-management-studio-ssms"></a>Abrir, exibir e imprimir um arquivo de deadlock no SQL Server Management Studio (SSMS)

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
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
  
  
