---
title: Como solucionar problemas de aprendizado de máquina no SQL Server
description: Fornece um ponto de partida para superar problemas no machine learning do SQL.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 05/31/2018
ms.topic: troubleshooting
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 036f4a7b604825f09dc884594e17c50396d84c0e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87253626"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>Como solucionar problemas de aprendizado de máquina no SQL Server
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

Use este artigo como um ponto de partida para solucionar problemas encontrados ao usar o machine learning do SQL Server.

## <a name="known-issues"></a>Problemas conhecidos

Os artigos a seguir descrevem problemas conhecidos com as versões atuais e anteriores:

+ [Problemas conhecidos do R Services](known-issues-for-sql-server-machine-learning-services.md)
+ [Notas de versão do SQL Server 2016](../../sql-server/sql-server-2016-release-notes.md)
+ [Notas de versão do SQL Server 2017](../../sql-server/sql-server-2017-release-notes.md)
+ [Notas sobre a versão do SQL Server 2019](../../sql-server/sql-server-version-15-release-notes.md)

## <a name="how-to-gather-system-information"></a>Como coletar informações do sistema

Se você encontrou um erro ou precisa entender um problema em seu ambiente, é importante que você colete as informações relacionadas sistematicamente. O artigo a seguir fornece uma lista de informações que facilitam a solução de problemas de autoajuda ou uma solicitação de suporte técnico.

+ [Coleta de dados para solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guias de instalação e configuração

Se você não tiver configurado o aprendizado de máquina com SQL Server ou se quiser adicionar o recurso, comece aqui:

+ [Instalar os Serviços de Machine Learning do SQL Server (no Banco de Dados)](../install/sql-machine-learning-services-windows-install.md)
+ [Instalar o Machine Learning Server do SQL Server (autônomo)](../install/sql-machine-learning-standalone-windows-install.md)
+ [Configuração de prompt de comando](../install/sql-ml-component-commandline-install.md)
+ [Instalação offline (sem Internet)](../install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuração

Os seguintes artigos contêm informações sobre padrões e sobre como personalizar a configuração do machine learning em uma instância SQL:

+ [Escalonar a execução simultânea de scripts externos nos Serviços de Machine Learning do SQL Server](../administration/scale-concurrent-execution-external-scripts.md)   
+ [Como criar um pool de recursos](../administration/create-external-resource-pool.md)
+ [Otimização para cargas de trabalho do R](../r/operationalizing-your-r-code.md)
