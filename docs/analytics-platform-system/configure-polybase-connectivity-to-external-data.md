---
title: Configurar a conectividade do polybase
description: Explica como configurar o polybase em paralelo data warehouse para se conectar a fontes de dados de blob de armazenamento do Hadoop ou Microsoft Azure externas. Use o polybase para executar consultas que integram dados de várias fontes, incluindo Hadoop, armazenamento de BLOBs do Azure e data warehouse paralelas.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 352f51e0d53c9dc145b1faf1832faf59587fef6f
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243087"
---
# <a name="configure-polybase-connectivity"></a>Configurar a conectividade do polybase
O polybase permite que o APS (sistema de plataforma de análise) processe consultas Transact-SQL que podem ler e gravar dados em fontes de dados externas. As mesmas consultas que acessam dados externos também podem incluir tabelas de relações em seus APS. Isso permite que você combine dados de fontes externas com dados relacionais de alto valor em seus bancos de dados APS.

![PolyBase lógico](media/polybase/polybase-logical.png)

O polybase no APS dá suporte à leitura e gravação no sistema de arquivos do Hadoop (HDFS) e ao armazenamento de BLOBs do Azure. O polybase também tem a capacidade de enviar alguns cálculos para nós do Hadoop como trabalhos MapReduce para otimizar o desempenho geral da consulta. O polybase no APS pode operar em texto delimitado, arquivos ORC e parquet. Veja [o que é o polybase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) para obter uma descrição completa e seus recursos.

> [!NOTE]
> Atualmente, os APS dão suporte apenas ao armazenamento de BLOBs do Azure com redundância local (LRS) padrão de uso geral v1.

## <a name="features-and-limitations"></a>Recursos e limitações
Consulte os [recursos e a limitação](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary) para obter um resumo dos recursos do polybase disponíveis e limitações conhecidas em APS e outros produtos SQL Server.

> [!NOTE] 
> O restante dos artigos relacionados ao polybase descrevem como configurar o polybase no APS 2016 (AU6) e posterior.

## <a name="see-also"></a>Consulte Também
- [Hadoop](polybase-configure-hadoop.md)
- [Armazenamento de Blobs do Azure](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
