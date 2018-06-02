---
title: Configurar e gerenciar instâncias do serviço de aprendizado de máquina do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b24832c8debe12c11aaa337e9558d99e7fae5ae0
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585498"
---
# <a name="configure-and-manage-machine-learning-components-in-sql-server"></a>Configurar e gerenciar os componentes de aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo fornece links para informações mais detalhadas sobre como configurar um servidor para oferecer suporte a serviços de aprendizado de máquina com o SQL Server nesses produtos:

+ SQL Server 2016 R Services (no banco de dados)
+ Serviços de aprendizado de máquina do SQL Server de 2017 (no banco de dados)

> [!NOTE]
> 
> Este conteúdo foi gravado originalmente para a versão de 2016 do SQL Server, que tem suporte apenas a linguagem R.
> 
> No SQL Server de 2017, o suporte para Python foi adicionado, mas a estrutura subjacente de arquitetura e serviços é o mesmo. Portanto, você pode configurar a segurança, memória, governança de recursos e outras opções para permitir a execução de scripts de Python, da mesma maneira que faria para scripts de R.
> 
> No entanto, como suporte para Python é um novo recurso, as informações detalhadas sobre otimizações potenciais para a carga de trabalho do Python ainda não está disponível. Verifique novamente mais tarde.

## <a name="r-package-management"></a>Gerenciamento de pacotes de R

Esses artigos descrevem como instalar novos pacotes de R na instância do SQL Server, gerenciar bibliotecas de pacote de R e bibliotecas do pacote de restauração após uma restauração de banco de dados.

+ [Pacotes R padrão e Python no SQL Server](installing-and-managing-r-packages.md)
+ [Instalar novos pacotes de R](install-additional-r-packages-on-sql-server.md)
+ [Habilitar o gerenciamento de pacotes para uma instância usando as funções de banco de dados](r-package-how-to-enable-or-disable.md)
+ [Criar um repositório Local do pacote usando miniCRAN](create-a-local-package-repository-using-minicran.md)
+ [Determinar que quais pacotes de R são instalados no SQl Server](determine-which-packages-are-installed-on-sql-server.md)
+ [Sincronização de pacotes de R entre o SQL Server e o sistema de arquivos](package-install-uninstall-and-sync.md)
+ [Pacotes R instalados nas bibliotecas de usuário](packages-installed-in-user-libraries.md)

## <a name="service-configuration"></a>Configuração do serviço

Esses artigos descrevem como fazer alterações na arquitetura de serviço subjacente e como gerenciar entidades de segurança associadas ao serviço de extensibilidade.

+ [Considerações sobre segurança](security-considerations-for-the-r-runtime-in-sql-server.md)
+ [Modificar o pool de contas de usuário para o SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)
+ [Configurar e gerenciar Extensões de Análise Avançada](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)
+ [Habilitar o gerenciamento de pacotes para uma instância usando as funções de banco de dados](r-package-how-to-enable-or-disable.md)
+ [Ajuste de desempenho para serviços de R](sql-server-r-services-performance-tuning.md)

## <a name="resource-governance"></a>Governança de recursos

Esses artigos descrevem como implementar o gerenciamento de recursos para trabalhos de R ou Python usando o administrador de recursos recurso disponível na edição Enterprise.

+ [Governança de recursos para o R Services](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [Como criar um Pool de recursos para R](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

Consulte também:

+ [Monitor R usando os relatórios personalizados do SSMS](monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="initial-setup"></a>Instalação inicial

Ajuda adicionais relacionadas à instalação e configuração inicial pode ser encontrada neste artigo:

+ [Perguntas frequentes sobre atualização e instalação](../r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [Considerações sobre segurança](../r/security-considerations-for-the-r-runtime-in-sql-server.md)
+ [Problemas conhecidos do R Services](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)

