---
title: Solução de problemas
description: Fornece um ponto de partida para trabalhar com problemas conhecidos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 16f85f78caed45119003d420636a90d226df127d
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2020
ms.locfileid: "81118179"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>Como solucionar problemas de aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use este artigo como um ponto de partida para trabalhar com problemas conhecidos.

## <a name="known-issues"></a>Problemas conhecidos

Os artigos a seguir descrevem problemas conhecidos com as versões atuais e anteriores:

+ [Problemas conhecidos do R Services](../machine-learning/known-issues-for-sql-server-machine-learning-services.md)
+ [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
+ [Notas de versão do SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>Como coletar informações do sistema

Se você encontrou um erro ou precisa entender um problema em seu ambiente, é importante que você colete as informações relacionadas sistematicamente. O artigo a seguir fornece uma lista de informações que facilitam a solução de problemas de autoajuda ou uma solicitação de suporte técnico.

+ [Coleta de dados para solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guias de instalação e configuração

Se você não tiver configurado o aprendizado de máquina com SQL Server ou se quiser adicionar o recurso, comece aqui:

+ [Instalar os Serviços de Machine Learning do SQL Server (no Banco de Dados)](install/sql-machine-learning-services-windows-install.md)
+ [Instalar o Machine Learning Server do SQL Server (autônomo)](install/sql-machine-learning-standalone-windows-install.md)
+ [Configuração de prompt de comando](install/sql-ml-component-commandline-install.md)
+ [Instalação offline (sem Internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuração

Os artigos a seguir contêm informações sobre padrões e sobre como personalizar a configuração do aprendizado de máquina em uma instância:

+ [Escalonar a execução simultânea de scripts externos nos Serviços de Machine Learning do SQL Server](administration/scale-concurrent-execution-external-scripts.md)   
+ [Como criar um pool de recursos](administration/create-external-resource-pool.md)
+ [Otimização para cargas de trabalho do R](r/operationalizing-your-r-code.md)
