---
title: Fazer upgrade do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
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
manager: jroth
ms.openlocfilehash: 029643d80f98f22e49e567bde8a2fb6e85073e50
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66794744"
---
# <a name="upgrade-database-engine"></a>Atualizar o Mecanismo de Banco de Dados

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  Os artigos nesta seção ajudarão você a atualizar o mecanismo de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma versão anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a versão [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
1.  [Escolha um Método de Atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md) Antes de iniciar uma atualização, você precisa entender os vários métodos de atualização. Este artigo aborda os métodos de atualização e as etapas envolvidas em cada método de atualização.  
  
2.  [Planejar e testar o plano de atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md) Depois de examinar os métodos de atualização, você estará pronto para desenvolver o método de atualização apropriado para seu ambiente e, em seguida, testar o método de atualização antes de atualizar o ambiente existente. Este artigo discute o desenvolvimento de um plano de atualização e como testá-lo.  
  
3.  [Concluir a Atualização do Mecanismo de Banco de Dados](../../database-engine/install-windows/complete-the-database-engine-upgrade.md) Depois que seus bancos de dados tiverem sido atualizados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], haverá etapas adicionais necessárias, incluindo um novo backup, habilitar recursos e repopular os catálogos de texto completo. Este artigo discute essas etapas.  
  
4.  [Alterar o modo de compatibilidade do banco de dados e usar o repositório de consultas](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md) Uma das etapas a serem seguidas após a atualização de seus bancos de dados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] é habilitar novos recursos alterando o modo de compatibilidade do banco de dados e usar o repositório de consultas para monitorar o desempenho. Este artigo aborda este processo e fornece um fluxo de trabalho recomendado.  
  
5.  [Aproveitar os novos recursos do SQL Server](https://www.microsoft.com/sql-server/sql-server-2017) Por fim, depois de concluir as etapas anteriores, você estará pronto para explorar, aproveitando as vantagens de novas melhorias específicas do mecanismo de banco de dados. Este artigo sugere alguns desses aperfeiçoamentos e fornece links para mais informações.  
  
  
