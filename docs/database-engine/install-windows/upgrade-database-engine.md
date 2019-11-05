---
title: Fazer upgrade do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 7dcf58da00887f396568367982da97b9c75e32ad
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531561"
---
# <a name="upgrade-database-engine"></a>Atualizar o Mecanismo de Banco de Dados

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
  Os artigos nesta seção ajudarão você a atualizar o mecanismo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma versão anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
1.  [Escolher um método de atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md). Antes de iniciar uma atualização, você precisa entender os vários métodos de atualização. Este artigo aborda os métodos de atualização e as etapas envolvidas em cada método de atualização.  
  
2.  [Planejar e testar o plano de atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md). Depois de examinar os métodos de atualização, você estará pronto para desenvolver o método de atualização apropriado para seu ambiente e, em seguida, testar o método de atualização antes de atualizar o ambiente existente. Este artigo discute o desenvolvimento de um plano de atualização e como testá-lo.  
  
3.  [Concluir a atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/complete-the-database-engine-upgrade.md). Depois que seu mecanismo de banco de dados tiver sido atualizado para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e os bancos de dados estiverem online, haverá etapas adicionais que precisarão ser seguidas, incluindo realizar um novo backup, atualizar a funcionalidade de bancos de dados para habilitar novos recursos e repopular catálogos de texto completo. Este artigo discute essas etapas.  
  
4.  Atualize o [Nível de compatibilidade do banco de dados](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades) (**Aplica-se a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]). Uma das etapas a ser seguida depois que seus bancos de dados estiverem online na nova versão de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] pode ser atualizar o modo de funcionalidade dos bancos de dados para habilitar novos recursos, por meio da alteração do nível de compatibilidade do banco de dados. Isso pode ser feito manualmente ou por meio do Assistente de Ajuste de Consulta. 

    - [Altere o modo de compatibilidade do banco de dados e use o Repositório de Consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md). Após alterar manualmente o nível de compatibilidade do banco de dados, use o Repositório de Consultas para monitorar o desempenho e identificar possíveis regressões. Este artigo aborda o processo recomendado e fornece um fluxo de trabalho recomendado.  

    - [Altere o modo de compatibilidade do banco de dados com o Assistente de Ajuste de Consulta](../../relational-databases/performance/upgrade-dbcompat-using-qta.md). Como alternativa a uma alteração manual, use o **QTA (Assistente de Ajuste de Consulta)** para ser guiado no processo recomendado de alteração do nível de compatibilidade do banco de dados. Este artigo aborda esse processo e fornece instruções sobre o fluxo de trabalho do QTA.  

    Para saber mais sobre novos recursos e melhores comportamentos disponíveis após alterar um nível de compatibilidade do banco de dados, confira [Diferenças entre níveis de compatibilidade](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-stored-procedures).

5.  [Aproveite os Novos Recursos do SQL Server](https://www.microsoft.com/sql-server/sql-server-2019). Por fim, depois de concluir as etapas anteriores, você estará pronto para explorar, aproveitando as vantagens de novos aprimoramentos específicos do mecanismo de banco de dados. Este artigo sugere alguns desses aperfeiçoamentos e fornece links para mais informações.  
  
  
