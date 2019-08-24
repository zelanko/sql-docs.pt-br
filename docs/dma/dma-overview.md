---
title: Visão geral de Assistente de Migração de Dados (SQL Server) | Microsoft Docs
description: Saiba como usar Assistente de Migração de Dados para migrar bancos de dados do SQL Server para outros bancos de dados do SQL Server ou do Azure
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: 26a8dbc4a156b8910bd35dfb7381608ec7198f78
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000600"
---
# <a name="overview-of-data-migration-assistant"></a>Visão geral do Assistente de Migração de Dados
O Assistente de Migração de Dados (DMA) ajuda você a atualizar para uma plataforma de dados moderna detectando problemas de compatibilidade que podem afetar a funcionalidade do banco de dado em sua nova versão do SQL Server ou do banco de dados SQL do Azure. O DMA recomenda melhorias de desempenho e confiabilidade para seu ambiente de destino e permite que você mova o esquema, os dados e os objetos não contidos do seu servidor de origem para o servidor de destino.

> [!NOTE] 
> Para grandes migrações (em termos de número e tamanho de bancos de dados), é recomendável que você use o [serviço de migração de banco de dados do Azure](/azure/dms/dms-overview), que pode migrar bancos de dados em escala.
  
## <a name="get-data-migration-assistant"></a>Obter o Assistente de Migração de Dados
Para instalar o DMA, baixe a versão mais recente da ferramenta no [centro de download da Microsoft](https://www.microsoft.com/download/details.aspx?id=53595)e, em seguida, execute o arquivo **DataMigrationAssistant. msi** .

## <a name="capabilities"></a>Capacidades
- Avaliar instâncias de SQL Server locais migrando para os bancos de dados SQL do Azure. O fluxo de trabalho de avaliação ajuda a detectar os seguintes problemas que podem afetar a migração do banco de dados SQL do Azure e fornece orientações detalhadas sobre como resolvê-los.

  - Problemas de bloqueio de migração: Descobre os problemas de compatibilidade que bloqueiam a migração de bancos de dados locais SQL Server para bancos de dados SQL do Azure. O DMA fornece recomendações para ajudá-lo a resolver esses problemas.

  - Recursos com suporte parcial ou sem suporte: Detecta recursos com suporte parcial ou sem suporte que estão em uso no momento na instância de SQL Server de origem. O DMA fornece um conjunto abrangente de recomendações, abordagens alternativas disponíveis no Azure e atenuação de etapas para que você possa incorporá-las em seus projetos de migração.

- Descubra problemas que podem afetar uma atualização para um SQL Server local. Eles são descritos como problemas de compatibilidade e são organizados nas seguintes categorias:

  - Alterações recentes
  - Alterações de comportamento
  - Recursos preteridos

- Descubra novos recursos na plataforma de SQL Server de destino para os quais o banco de dados pode se beneficiar após uma atualização. Elas são descritas como recomendações de recursos e são organizadas nas seguintes categorias:

  - Desempenho
  - Segurança
  - Armazenamento

- Migre uma instância de SQL Server local para uma instância moderna do SQL Server hospedada localmente ou em uma VM (máquina virtual) do Azure que possa ser acessada por sua rede local. A VM do Azure pode ser acessada usando VPN ou outras tecnologias. O fluxo de trabalho de migração ajuda a migrar os seguintes componentes:

  - Esquema de bancos de dados
  - Dados e usuários
  - Funções de servidor
  - Logons SQL Server e do Windows

- Após uma migração bem-sucedida, os aplicativos podem se conectar aos bancos de dados de SQL Server de destino diretamente.

- Avaliar pacotes do SQL Server Integration Services (SSIS) locais migrando para o banco de dados SQL do Azure ou a instância gerenciada do banco de dados SQL do Azure. A avaliação ajuda a descobrir problemas que podem afetar a migração. Eles são descritos como problemas de compatibilidade e são organizados nas seguintes categorias:

  - Bloqueadores de migração: descobre os problemas de compatibilidade que bloqueiam a migração de pacote (s) de origem para o Azure. O DMA fornece recomendações para ajudá-lo a resolver esses problemas.

  - Problemas de informação: detecta recursos com suporte parcial ou preteridos que são usados em pacotes de origem.

  > [!NOTE]
  > A avaliação de pacotes hospedados no sistema de arquivos só tem suporte.
  > A avaliação de pacotes hospedados no MSDB, no repositório de pacotes ou no SSISDB vem mais tarde.

## <a name="prerequisites"></a>Pré-requisitos
Para executar uma avaliação, você precisa ser membro da função SQL Server **sysadmin** .

## <a name="supported-source-and-target-versions"></a>Versões de origem e de destino com suporte
O DMA substitui todas as versões anteriores do supervisor de atualização do SQL Server e deve ser usado para atualizações para a maioria das versões de SQL Server. As versões de origem e destino com suporte são:

**Causas**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 no Windows

**Aos**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 no Windows e no Linux
- Banco de dados SQL do Azure
- Instância Gerenciada do Banco de Dados SQL do Azure

## <a name="see-also"></a>Confira também
[Avaliar sua migração de SQL Server](../dma/dma-assesssqlonprem.md)     
[Assistente de Migração de Dados: Definições de configuração](../dma/dma-configurationsettings.md)     
[Migrar SQL Server locais usando Assistente de Migração de Dados](../dma/dma-migrateonpremsql.md)     
[Assistente de Migração de Dados: Práticas recomendadas](../dma/dma-bestpractices.md)     
