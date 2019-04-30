---
title: Configurar a conectividade do PolyBase - Analytics Platform System | Microsoft Docs
description: Explica como configurar o PolyBase no Parallel Data Warehouse para se conectar ao Hadoop ou no Microsoft Azure storage blob fontes de dados externas. Usar o PolyBase para executar consultas que integram dados de várias fontes, incluindo Hadoop, o armazenamento de BLOBs do Azure e Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: da6d71521f72ff23b4caf2f27dbc663dee684592
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057797"
---
# <a name="what-is-polybase"></a>O que é o PolyBase?
O PolyBase permite que seu sistema APS (Analytics Platform) para processar consultas Transact-SQL que podem ler e gravar dados em fontes de dados externas. As mesmas consultas que acessam dados externos também podem incluir tabelas de relação em seus PAS. Isso permite que você combine dados de fontes externas com dados relacionais em seus bancos de dados de pontos de acesso de alto valor.

![PolyBase lógico](media/polybase/polybase-logical.png)

PolyBase nos APS dá suporte à leitura e gravação para o sistema de arquivos Hadoop (HDFS) e o armazenamento de BLOBs do Azure. O PolyBase também tem a capacidade de enviar por push uma computação para nós do Hadoop como trabalhos de mapreduce para otimizar o desempenho geral da consulta. O PolyBase no APS pode operar em texto delimitado, ORC e Parquet arquivos. Ver [o que é PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide) para uma descrição completa e seus recursos.

> [!NOTE]
> APS atualmente suporta apenas padrão uso geral v1 localmente redundante (LRS) Azure Blob Storage.

## <a name="features-and-limitations"></a>Recursos e limitações
Ver [recursos e limitação](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-versioned-feature-summary) para um resumo do PolyBase possui limitações conhecidas e disponíveis nos pontos de acesso e outros produtos do SQL Server.

> [!NOTE] 
> O restante do PolyBase relacionados artigos descrevem como configurar o PolyBase no APS 2016 (AU6) e versões posteriores.

## <a name="see-also"></a>Consulte também
- [Hadoop](polybase-configure-hadoop.md)
- [Armazenamento de Blobs do Azure](polybase-configure-azure-blob-storage.md)
<!-- MISSING LINKS [PolyBase &#40;SQL Server PDW&#41;](../sqlpdw/polybase-sql-server-pdw.md)  -->  
  
