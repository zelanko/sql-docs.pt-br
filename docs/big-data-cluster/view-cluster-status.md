---
title: Recursos de administração para BDCs (Clusters de Big Data)
titleSuffix: SQL Server
description: Esse artigo explica como ver o status de um cluster de Big Data usando o Azure Data Studio, notebooks e comandos da CLI de Dados do Azure (azdata).
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 10/20/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d469d1b8d89b07748485c9df3f7f7905af52099
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358124"
---
# <a name="administration-resources-for-big-data-clusters-bdc"></a>Recursos de administração para BDCs (Clusters de Big Data) 

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve como administrar um cluster de Big Data do SQL Server de fora pra dentro.

## <a name="know-your-architecture"></a>Conheça a sua arquitetura

Começando no SQL Server 2019 (15.x), os Clusters de Big Data do SQL Server permitem implantar clusters escalonáveis de contêineres do SQL Server, do Spark e do HDFS em execução no Kubernetes. Os seguintes artigos obtêm uma visão geral do cluster de Big Data:
- [O que são os Clusters de Big Data do SQL Server?](big-data-cluster-overview.md)

Os Clusters de Big Data do SQL Server fornecem autenticação e autorização coerentes e consistentes. Os seguintes artigos obtêm uma visão geral da segurança do cluster de Big Data:
- [Conceitos de segurança para Clusters de Big Data do SQL Server](concept-security.md)

## <a name="manage-and-operate-with-tools"></a>Gerenciar e operar com ferramentas

Os seguintes artigos descrevem como gerenciar e operar o cluster de Big Data das seguintes maneiras: 

- [Conectar-se a um cluster de Big Data do SQL Server com o Azure Data Studio](connect-to-big-data-cluster.md)
- [Gerenciar clusters de Big Data para o painel do controlador do SQL Server](manage-with-controller-dashboard.md)
- [Gerenciar Clusters de Big Data do SQL Server com notebooks do Azure Data Studio](notebooks-manage-bdc.md)
- [Gerenciar BDCs (Clusters de Big Data) com notebooks](cluster-manage-notebooks.md)
- [Executar um notebook de exemplo usando o Spark](notebooks-tutorial-spark.md)

## <a name="monitor-with-tools"></a>Monitorar com ferramentas

Os seguintes artigos descrevem como monitorar o cluster de Big Data das seguintes maneiras: 

- [Monitorar cluster BDC com o Azure Data Studio](cluster-monitor-ads.md)
- [Monitorar cluster BDC com o utilitário Azdata](cluster-monitor-cmdlet.md)
- [Monitorar cluster BDC com o Painel do Grafana](cluster-monitor-grafana.md)
- [Monitorar cluster BDC com Jupyter notebooks e Azure Data Studio](cluster-monitor-notebooks.md)

## <a name="monitor-and-inspect-logs-with-notebooks"></a>Monitorar e inspecionar logs com notebooks

Os artigos a seguir listam muitos dos Jupyter notebooks que estão disponíveis no Azure Data Studio.

- [Monitorar o cluster com notebooks](cluster-monitor-notebooks.md)
- [Coletar e analisar logs no cluster com notebooks](cluster-logging-notebooks.md)

## <a name="big-data-clusters-troubleshooting-resources"></a>Recursos de solução de problemas de Clusters de Big Data

Os seguintes artigos descrevem como solucionar problemas de cluster de Big Data:

- [Solucionar problemas do cluster BDC com o utilitário kubectl](cluster-troubleshooting-commands.md) 
- [Solucionar problemas de notebook do pyspark](troubleshoot-pyspark-notebook.md)
- [Solucionar problemas de cluster BDC com Jupyter notebooks e ADS (Azure Data Studio)](cluster-troubleshooter-notebooks.md)
- [Restaurar permissões do HDFS](troubleshoot-hdfs-restore-admin.md)

Os seguintes artigos descrevem como solucionar problemas de cluster de Big Data implantados no modo de Active Directory:
- [Solucionar problemas do cluster BDC no modo Active Directory](troubleshoot-active-directory.md) 
- [Solucionar problemas de falha no logon do modo AD](troubleshoot-ad-login-failed-untrusted-domain.md)
- [Solucionar problemas de interrupção na implantação do modo AD](troubleshoot-ad-reverse-lookup-zone.md)

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md).