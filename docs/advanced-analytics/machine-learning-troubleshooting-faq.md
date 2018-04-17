---
title: Solução de problemas e perguntas Frequentes para o aprendizado de máquina no SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 80d153baed382c95c85793e1605b700c2719e13c
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="troubleshoot-machine-learning"></a>Solucionar problemas de aprendizado de máquina
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece links para solução de problemas para guias de configuração, problemas conhecidos e notas de versão. Outros artigos vinculados a este artigo fornecerá subsídio sobre otimização de desempenho para soluções de aprendizado de máquina no SQL Server.

Use esta página como ponto de partida para localizar problemas conhecidos, perguntas comuns de instalação e procedimentos para solução de problemas.

**Aplica-se a:** R Services do SQL Server 2016, SQL Server 2017 Services (R e Python) de aprendizado de máquina

## <a name="known-issues"></a>Problemas conhecidos

Os artigos a seguir listam os problemas conhecidos com a versão atual ou descrevem problemas com versões anteriores:

+ [Problemas conhecidos do R Services](../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)
+ [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
+ [Notas de versão do SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)

## <a name="troubleshooting-prerequisites"></a>Pré-requisitos de solução de problemas

Se você encontrou um erro ou precisa entender um problema em seu ambiente, é importante que você colete sistematicamente informações relacionadas. Essas informações incluem a versão, a edição, o contexto de segurança e o contexto de execução.

O artigo a seguir fornece uma lista de informações que facilita a solução de problemas de autoajuda, ou uma solicitação para obter suporte técnico.

+ [Coleta de dados para a solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)

## <a name="setup-and-configuration-guides"></a>Guias de instalação e configuração

Comece aqui se você não configurou o aprendizado de máquina com o SQL Server, ou se você deseja adicionar o recurso:

+ [Instale os serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados)](install/sql-machine-learning-services-windows-install.md)
+ [Instalar o servidor do aprendizado de máquina 2017 SQL Server (autônomo)](install/sql-machine-learning-standalone-windows-install.md)
+ [Instalar o SQL Server 2016 R Services (no banco de dados)](install/sql-r-services-windows-install.md)
+ [Instalar o SQL Server 2016R Server (autônomo)](install/sql-r-standalone-windows-install.md)
+ [Instalação de prompt de comando](install/sql-ml-component-commandline-install.md)
+ [Instalação offline (sem Internet)](install/sql-ml-component-install-without-internet-access.md)

### <a name="configuration"></a>Configuração

Os seguintes artigos contêm informações sobre os padrões e como personalizar a configuração em uma instância do aprendizado de máquina:

+ [Modificar o pool de conta de usuário do SQL Server R Services](r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [Configurar e gerenciar extensões de análise avançada](r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Como criar um pool de recursos](r/how-to-create-a-resource-pool-for-r.md)
+ [Otimização para cargas de trabalho de R](r/operationalizing-your-r-code.md)
