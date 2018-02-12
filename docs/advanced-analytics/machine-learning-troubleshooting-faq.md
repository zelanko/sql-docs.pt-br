---
title: "Solução de problemas e perguntas Frequentes para o aprendizado de máquina no SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 06/16/2017
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d334aefbd43bf17e776a8b75a09a2cef8448542d
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="troubleshoot-machine-learning"></a>Solucionar problemas de aprendizado de máquina
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece informações de solução de problemas relacionadas à configuração de recursos de aprendizado de máquina do SQL Server. As informações incluem links para guias de configuração, problemas conhecidos e notas de versão. Outros artigos vinculados a este artigo fornecerá subsídio sobre otimização de desempenho para soluções de aprendizado de máquina no SQL Server.

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

+ [Configurar serviços de R ou serviços de aprendizado de máquina com R](../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)
+ [Configurar os serviços de aprendizado de máquina com Python](../advanced-analytics/python/setup-python-machine-learning-services.md)
+ [Perguntas frequentes sobre a instalação](../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [Use SqlBindR para atualizar uma instância dos serviços do R](../advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

Os artigos a seguir descrevem as etapas adicionais necessárias para a instalação offline de recursos de aprendizado de máquina do SQL Server:

+ [Instalação autônoma dos serviços do R](../advanced-analytics/r/unattended-installs-of-sql-server-r-services.md) 
+ [Instalação autônoma dos serviços de aprendizado de máquina com Python](../advanced-analytics/python/unattended-installs-of-sql-server-python-services.md)

Se você precisa instalar a recursos em um computador com nenhuma conexão de Internet de aprendizado de máquina, use os links neste artigo para baixar os componentes de R e Python antes do início da instalação:

+ [Instalando os componentes de aprendizado de máquina sem acesso à Internet](../advanced-analytics/r/installing-ml-components-without-internet-access.md)

### <a name="configuration"></a>Configuração

Os seguintes artigos contêm informações sobre os padrões e como personalizar a configuração em uma instância do aprendizado de máquina:

+ [Modificar o pool de conta de usuário do SQL Server R Services](../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)  
+ [Configurar e gerenciar extensões de análise avançada](../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)  
+ [Como criar um pool de recursos](r/how-to-create-a-resource-pool-for-r.md)
+ [Otimização para cargas de trabalho de R](r/operationalizing-your-r-code.md)

## <a name="related-tools-and-services"></a>Serviços e ferramentas relacionadas

+ [Configurar o Microsoft Machine Learning servidor autônomo](../advanced-analytics/r/create-a-standalone-r-server.md)
+ [Configurar o servidor de R em uma VM do Azure](../advanced-analytics/r/provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)
+ [Instalar o R Server para Windows](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)
+ [Obter ferramentas R para Visual Studio](https://www.visualstudio.com/vs/rtvs/)
