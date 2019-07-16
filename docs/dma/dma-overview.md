---
title: Visão geral do Assistente de migração de dados (SQL Server) | Microsoft Docs
description: Saiba como usar o Assistente de migração de dados para migrar bancos de dados do SQL Server para outro SQL Server ou bancos de dados do Azure
ms.custom: ''
ms.date: 03/12/2019
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
ms.openlocfilehash: 9aaadf6f4226b2c9a457c7437412f35c1bbe20fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054712"
---
# <a name="overview-of-data-migration-assistant"></a>Visão geral do Assistente de migração de dados
O Assistente de DMA (Data Migration) o ajuda a que atualizar para uma plataforma de dados moderna, detectando problemas de compatibilidade que podem afetar a funcionalidade de banco de dados na nova versão do SQL Server ou banco de dados SQL. O DMA recomenda melhorias no desempenho e confiabilidade para seu ambiente de destino e permite que você mova seu esquema, dados e objetos não contidos do servidor de origem para o servidor de destino.

> [!NOTE] 
> Para grandes migrações (em termos de número e tamanho dos bancos de dados), é recomendável que você use o [serviço de migração de banco de dados do Azure](/azure/dms/dms-overview), que pode migrar bancos de dados em grande escala.
  
## <a name="get-data-migration-assistant"></a>Obter o Assistente de Migração de Dados
Para instalar o DMA, baixe a versão mais recente da ferramenta do [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595)e, em seguida, execute o **DataMigrationAssistant.msi** arquivo.

## <a name="capabilities"></a>Capacidades
- Avalie as instâncias do SQL Server local migrando para bancos de dados SQL do Azure. O fluxo de trabalho de avaliação ajuda você a detectar os seguintes problemas que podem afetar a migração de banco de dados SQL do Azure e fornece orientações detalhadas sobre como resolvê-los.

  - Problemas de bloqueio de migração: Descobre os problemas de compatibilidade que bloqueiam a migração no local do SQL Server bancos de dados de para bancos de dados SQL do Azure. O DMA fornece recomendações para ajudá-lo a resolver esses problemas.

  - Recursos parcialmente suportados ou sem suportados: Detecta parcialmente com suporte ou não há suporte para recursos que estão atualmente em uso na instância do SQL Server de origem. O DMA fornece que um conjunto abrangente de recomendações, abordagens alternativas disponíveis no Azure e etapas atenuantes para que você pode incorporá-las em seus projetos de migração.

- Descubra os problemas que podem afetar uma atualização para um SQL Server no local. Esses são descritos como problemas de compatibilidade e são organizados nas seguintes categorias:

  - Alterações significativas
  - Alterações de comportamento
  - Recursos preteridos

- Descubra os novos recursos na plataforma do SQL Server de destino que pode se beneficiar do banco de dados após uma atualização. Esses são descritos como recomendações de recurso e são organizados nas seguintes categorias:

  - Desempenho
  - Segurança
  - Armazenamento

- Migre uma instância do SQL Server local para um moderno do SQL Server instância hospedada no local ou em uma máquina virtual do Azure (VM) que é acessível a partir de sua rede local. A VM do Azure podem ser acessada usando VPN ou outras tecnologias. O fluxo de trabalho de migração ajuda você a migrar os seguintes componentes:

  - Esquema de bancos de dados
  - Dados e usuários
  - Funções de servidor
  - Logons do SQL Server e do Windows

- Após uma migração bem-sucedida, aplicativos podem se conectar aos bancos de dados de SQL Server de destino diretamente.

## <a name="prerequisites"></a>Pré-requisitos
Para executar uma avaliação, você precisa ser um membro do SQL Server **sysadmin** função.

## <a name="supported-source-and-target-versions"></a>Versões com suporte de origem e destino
DMA substitui todas as versões anteriores do Supervisor de atualização do SQL Server e deve ser usado para atualizações para a maioria das versões do SQL Server. Versões de origem e destino com suporte são:

**Fontes**
- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012 
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 no Windows

**Destinos**
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 no Windows e Linux
- Banco de dados SQL do Azure
- Instância Gerenciada do Banco de Dados SQL do Azure

## <a name="see-also"></a>Confira também
[Avaliar sua migração do SQL Server](../dma/dma-assesssqlonprem.md)     
[Assistente de migração de dados: Definições de configuração](../dma/dma-configurationsettings.md)     
[As migrações local SQL Server usando o Assistente de migração de dados](../dma/dma-migrateonpremsql.md)     
[Assistente de migração de dados: Práticas recomendadas](../dma/dma-bestpractices.md)     
