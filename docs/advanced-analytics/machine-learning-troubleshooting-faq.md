---
title: Solução de problemas e perguntas frequentes sobre o aprendizado de máquina
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 86c698420a64832e49cd6cbff5e6727896ec45f4
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470275"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>Solucionar problemas de aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use esta página como um ponto de partida para trabalhar com problemas conhecidos.

**Aplica-se a:** SQL Server 2016 R Services, SQL Server 2017 Serviços de Machine Learning (R e Python)

## <a name="known-issues"></a>Problemas conhecidos

Os artigos a seguir descrevem problemas conhecidos com as versões atuais e anteriores:

+ [Problemas conhecidos do R Services](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
+ [Notas de versão do SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>Como coletar informações do sistema

Se você encontrou um erro ou precisa entender um problema em seu ambiente, é importante que você colete informações relacionadas sistematicamente. O artigo a seguir fornece uma lista de informações que facilitam a solução de problemas de auto-ajuda ou uma solicitação de suporte técnico.

+ [Coleta de dados para solução de problemas de Machine Learning](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guias de instalação e configuração

Comece aqui se você não tiver configurado o aprendizado de máquina com SQL Server, ou se quiser adicionar o recurso:

+ [Instalar SQL Server 2017 Serviços de Machine Learning (no banco de dados)](install/sql-machine-learning-services-windows-install.md)
+ [Instalar o SQL Server 2017 Machine Learning Server (autônomo)](install/sql-machine-learning-standalone-windows-install.md)
+ [Instalar o SQL Server R Services 2016 (no banco de dados)](install/sql-r-services-windows-install.md)
+ [Instalar o SQL Server R Server 2016 (autônomo)](install/sql-r-standalone-windows-install.md)
+ [Instalação do prompt de comando](install/sql-ml-component-commandline-install.md)
+ [Instalação offline (sem Internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuração

Os artigos a seguir contêm informações sobre padrões e como personalizar a configuração do Machine Learning em uma instância do:

+ [Dimensionar a execução simultânea de scripts externos no SQL Server Serviços de Machine Learning](administration/modify-user-account-pool.md)   
+ [Configurar e gerenciar extensões de análise avançada](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Como criar um pool de recursos](r/how-to-create-a-resource-pool-for-r.md)
+ [Otimização para cargas de trabalho do R](r/operationalizing-your-r-code.md)
