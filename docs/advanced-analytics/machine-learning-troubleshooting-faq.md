---
title: Solução de problemas e perguntas Frequentes para o aprendizado de máquina - serviços de aprendizado de máquina do SQL Server
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4a62dd0710a97a33f5a4703f194df2c6bcef2a54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62650323"
---
# <a name="troubleshoot-machine-learning-in-sql-server"></a>Solucionar problemas de aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Use esta página como ponto de partida para trabalhar com os problemas conhecidos.

**Aplica-se a:** SQL Server 2016 R Services, SQL Server 2017 serviços de Machine Learning (R e Python)

## <a name="known-issues"></a>Problemas conhecidos

Os artigos a seguir descrevem problemas conhecidos com as versões atuais e anteriores:

+ [Problemas conhecidos para o R Services](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
+ [Notas de versão do SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)

## <a name="how-to-gather-system-information"></a>Como coletar informações do sistema

Se você encontrou um erro ou precisa compreender um problema em seu ambiente, é importante que você colete informações relacionadas sistematicamente. O artigo a seguir fornece uma lista de informações que facilita a solução de problemas de auto-ajuda ou uma solicitação para obter suporte técnico.

+ [Coleta de dados para a solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guias de instalação e configuração

Comece aqui se você não tiver configurado o aprendizado de máquina com o SQL Server, ou se você deseja adicionar o recurso:

+ [Instalar serviços de Machine Learning do SQL Server 2017 (no banco de dados)](install/sql-machine-learning-services-windows-install.md)
+ [Instalar o SQL Server 2017 Machine Learning Server (autônomo)](install/sql-machine-learning-standalone-windows-install.md)
+ [Instalar o SQL Server 2016 R Services (no banco de dados)](install/sql-r-services-windows-install.md)
+ [Instalar o SQL Server 2016 R Server (autônomo)](install/sql-r-standalone-windows-install.md)
+ [Instalação de prompt de comando](install/sql-ml-component-commandline-install.md)
+ [Instalação offline (sem Internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuração

Os seguintes artigos contêm informações sobre os padrões e como personalizar a configuração para uma instância de aprendizado de máquina:

+ [Escala de execução simultânea de scripts externos em serviços do SQL Server Machine Learning](administration/modify-user-account-pool.md)   
+ [Configurar e gerenciar extensões de análise avançada](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Como criar um pool de recursos](r/how-to-create-a-resource-pool-for-r.md)
+ [Otimização para cargas de trabalho de R](r/operationalizing-your-r-code.md)
