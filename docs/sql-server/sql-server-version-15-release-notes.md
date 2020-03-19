---
title: Notas sobre a versão do SQL Server 2019 | Microsoft Docs
description: Encontre informações sobre limitações, problemas conhecidos, recursos de ajuda e outras notas sobre a versão do SQL Server 2019 (15.x).
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 0d27209448ece622a4906f6ba2cae28268c0210a
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79190604"
---
# <a name="sql-server-2019-release-notes"></a>Notas sobre a versão do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve as limitações e problemas conhecidos do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]. Para obter informações relacionadas. consulte:

> [Novidades no [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]](../sql-server/what-s-new-in-sql-server-ver15.md)

## [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

A [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] é a última versão pública do [!INCLUDE[SQL Server 2019](../includes/ssnoversion-md.md)].

Detalhes completos sobre o licenciamento estão na pasta `License Terms` na mídia de instalação.

## <a name="documentation"></a>Documentação

- **Problema e impacto para o cliente**: a documentação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode ser filtrada por versão. Use o controle na parte superior esquerda de cada página de documentação para filtrar os requisitos.

## <a name="build-number"></a>Número de build

O número de build de RTM para SQL Server 2019 é `15.0.2000.5`.

[!INCLUDE [sql-server-servicing-updates-version-15](../includes/sql-server-servicing-updates-version-15.md)]

## <a name="sql-server-installation-may-fail-if-ssms-18x-is-installed"></a>A instalação do SQL Server poderá falhar se o SSMS 18.x estiver instalado

- **Problema e impacto no cliente**: a instalação do [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] falhará quando as seguintes instalações ocorrerem nesta ordem:
  1. SSMS (SQL Server Management Studio) versão 18.0, 18.1, 18.2 ou 18.3 está instalado no servidor.
  1. a instalação de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] é tentada a partir da mídia removível. Por exemplo, a mídia de instalação é um DVD.

- **Solução alternativa**:
  1. Desinstale todas as versões do SSMS mais antigas que o SSMS 18.3.1.
  1. Instale uma versão mais recente do SSMS (18.3.1 ou posterior). Para obter a versão mais recente, confira [Baixar o SSMS](../ssms/download-sql-server-management-studio-ssms.md).
  1. Instale o [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] normalmente.

- **Aplica-se ao**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]

## <a name="utf-8-collations"></a>Ordenações UTF-8

- **Problema e impacto sobre o cliente**: Os agrupamentos de UTF-8 habilitados não poderão ser usados com os seguintes recursos:
  - [Tabelas de OLTP in-memory](../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)
  - [Always Encrypted com enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md) (quando não estiver usando enclaves seguros, o [Always Encrypted](../relational-databases/security/encryption/always-encrypted-database-engine.md) pode usar UTF-8)

  > [!WARNING]
  > A criação de um [bacpac](../relational-databases/data-tier-applications/data-tier-applications.md#bacpac) de um banco de dados que contém colunas de tabela definidas como [CHAR ou VARCHAR](../t-sql/data-types/char-and-varchar-transact-sql.md) que usam mais de 4 mil bytes falhará.
  
  > [!NOTE]
  > No momento, não há nenhuma interface do usuário compatível para escolher as ordenações UTF-8 habilitadas no Azure Data Studio ou SSDT (SQL Server Data Tools). A versão 18 do SSMS ([!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]) mais recente dá suporte à seleção de ordenações habilitadas para UTF-8 na interface do usuário.

- **Aplica-se ao**: RTM [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]

## <a name="master-data-service-notification-email-contains-broken-link"></a>O email de notificações do Master Data Services contém um link desfeito

- **Problema e impacto sobre o cliente**: O email de notificação do MDS (Master Data Services) contém um link desfeito. O link navega até uma página que retorna um erro como a seguinte mensagem:

   `The view 'Index' or its master was not found or no view engine supports the searched locations.`

- **Solução alternativa**: Abra o portal do MDS e acesse o recurso manualmente.

- **Aplica-se ao**: RTM [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]

## <a name="see-also"></a>Confira também

- [Requisitos de Hardware e Software para a Instalação do SQL Server](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)

## <a name="machine-learning-services"></a>Serviços de Machine Learning

Para problemas nos Serviços de Machine Learning do SQL Server, confira [Problemas conhecidos nos Serviços de Machine Learning do SQL Server](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md).

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]
