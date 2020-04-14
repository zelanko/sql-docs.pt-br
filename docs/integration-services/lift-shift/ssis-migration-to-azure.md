---
title: Visão geral da migração do SQL Server Integration Services para o Azure | Microsoft Docs
description: Este artigo destaca o processo e as ferramentas para migrar o SQL Server Integration Services para o Azure.
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 81fb9b9cb792cf350137a375e7a2e25643656b6e
ms.sourcegitcommit: 335d27d0493ddf4ffb770e13f8fe8802208d25ae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/09/2020
ms.locfileid: "81002847"
---
# <a name="migrate-on-premises-ssis-workloads-to-ssis-in-adf"></a>Migrar cargas de trabalho do SSIS local para o SSIS no ADF

Este artigo lista o processo e as ferramentas que podem ajudar a migrar cargas de trabalho do SSIS (SQL Server Integration Services) para o SSIS no ADF.

A [Visão geral da migração](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview) destaca o processo de migração geral das cargas de trabalho ETL do SSIS local para o SSIS no ADF.

O processo de migração consiste em duas fases: [Avaliação](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview#assessment) e [Migração](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview#migration).

## <a name="assessment"></a>Avaliação

O AMD (Assistente de Migração de Dados) é uma ferramenta gratuita que pode ser baixada para essa finalidade e ser instalada e executada localmente. Um projeto de avaliação do AMD do tipo Integration Services pode ser criado para avaliar pacotes SSIS em lotes e identificar problemas de compatibilidade.

Obtenha o [Assistente de Migração de Banco de Dados](https://docs.microsoft.com/sql/dma/dma-overview) e [execute a avaliação de pacote](https://docs.microsoft.com/sql/dma/dma-assess-ssis).

## <a name="migration"></a>Migração

Dependendo dos tipos de armazenamento dos pacotes SSIS de origem e do destino de migração das cargas de trabalho de banco de dados, as etapas para migrar os pacotes SSIS e os trabalhos do SQL Server Agent que agendam as execuções de pacote SSIS podem variar. Para obter mais informações, consulte [esta página](https://docs.microsoft.com/azure/data-factory/scenario-ssis-migration-overview#migration).

## <a name="next-steps"></a>Próximas etapas

- [Migrar pacotes SSIS para uma Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/dms/how-to-migrate-ssis-packages-managed-instance).
- [Migrar trabalhos do SSIS para o ADF (Azure Data Factory) com o SSMS (SQL Server Management Studio)](https://docs.microsoft.com/azure/data-factory/how-to-migrate-ssis-job-ssms).
