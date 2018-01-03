---
title: "Configuração e gerenciamento | Microsoft Docs"
ms.custom: 
ms.date: 05/31/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0fd4554-60c6-4181-ac4c-2e366fb434f6
caps.latest.revision: "7"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 075434e13ad8e988041eee360674ffcb59729312
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="configuration-and-management"></a>Configuração e gerenciamento

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

Estes tópicos descrevem como instalar novos pacotes de R na instância do SQL Server, gerenciar bibliotecas de pacote de R e bibliotecas do pacote de restauração após uma restauração de banco de dados.

+ [Instalar e gerenciar pacotes do R](installing-and-managing-r-packages.md)
+ [Instalar novos pacotes de R](install-additional-r-packages-on-sql-server.md)
+ [Habilitar o gerenciamento de pacotes para uma instância usando as funções de banco de dados](r-package-how-to-enable-or-disable.md)
+ [Criar um repositório Local do pacote usando miniCRAN](create-a-local-package-repository-using-minicran.md)
+ [Determinar que quais pacotes de R são instalados no SQl Server](determine-which-packages-are-installed-on-sql-server.md)
+ [Sincronização de pacotes de R entre o SQL Server e o sistema de arquivos](package-install-uninstall-and-sync.md)
+ [Pacotes R instalados nas bibliotecas de usuário](packages-installed-in-user-libraries.md)

## <a name="service-configuration"></a>Configuração do serviço

Estes tópicos descrevem como fazer alterações na arquitetura de serviço subjacente e como gerenciar entidades de segurança associadas ao serviço de extensibilidade.

+ [Considerações sobre segurança](security-considerations-for-the-r-runtime-in-sql-server.md)
+ [Modificar o pool de contas de usuário para o SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md)
+ [Configurar e gerenciar Extensões de Análise Avançada](../../advanced-analytics/r/configure-and-manage-advanced-analytics-extensions.md)
+ [Habilitar o gerenciamento de pacotes para uma instância usando as funções de banco de dados](r-package-how-to-enable-or-disable.md)
+ [Ajuste de desempenho para serviços de R](sql-server-r-services-performance-tuning.md)

## <a name="resource-governance"></a>Governança de recursos

Estes tópicos descrevem como implementar o gerenciamento de recursos para trabalhos de R ou Python usando o administrador de recursos recurso disponível na edição Enterprise.

+ [Governança de recursos para o R Services](../../advanced-analytics/r/resource-governance-for-r-services.md)
+ [Como criar um Pool de recursos para R](../../advanced-analytics/r/how-to-create-a-resource-pool-for-r.md)

Consulte também:

+ [Monitor R usando os relatórios personalizados do SSMS](monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="initial-setup"></a>Instalação inicial

Ajuda adicionais relacionadas à instalação e configuração inicial pode ser encontrada nestes tópicos:

+ [Perguntas frequentes sobre atualização e instalação](../r/upgrade-and-installation-faq-sql-server-r-services.md)
+ [Considerações sobre segurança](../r/security-considerations-for-the-r-runtime-in-sql-server.md)
+ [Problemas conhecidos do R Services](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)

