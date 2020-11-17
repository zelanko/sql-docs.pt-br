---
title: 'Assistente para adicionar réplica: Página inserir senhas para grupos de disponibilidade'
description: Uma descrição das propriedades encontradas na 'página Inserir senha' do Assistente para adicionar réplica no SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: end-user-help
f1_keywords:
- sql13.swb.addreplicawizard.enterpasswords.f1
ms.assetid: e69207a0-c5c4-44e4-ae9a-4afbb67251d1
author: cawrites
ms.author: chadam
ms.openlocfilehash: 4ab6d424bfa1ff70ada91956e4552032843ff28b
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584258"
---
# <a name="enter-passwords-page-add-replica-wizard-for-always-on-availability-groups"></a>Página Inserir senhas (Assistente para adicionar réplica) para grupos de disponibilidade Always On
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Este tópico da ajuda descreve as opções da página **Inserir Senhas** . Este tópico aplica-se ao [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 Se as réplicas escolhidas na página **Especificar Réplicas** tiver bancos de dados com uma chave mestra do banco de dados, a página Inserir Senhas aparecerá.  
  
## <a name="enter-passwords-options"></a>Opções para Inserir Senhas  
 A grade **Bancos de dados de usuário nesta instância do SQL Server** lista todos os bancos de dados de usuário locais. As colunas são apresentadas assim:  
  
 **Nome**  
 Exibe o nome do banco de dados de usuário local.  
  
 **Tamanho**  
 Exibe o tamanho do banco de dados, se o tamanho estiver disponível para o assistente.  
  
 **Status**  
 Indica a **Senha necessária** para os bancos de dados que têm uma chave mestra do banco de dados. Depois de inserir as senhas para as chaves mestras do banco de dados na coluna **Senhas** , clique em **Atualizar**. Se você tiver digitado as senhas corretamente, a coluna **Status** indicará **Senha digitada**.  
  
 Se o banco de dados não tiver uma chave mestra do banco de dados, a coluna **Status** indicará **Senha não necessária**.  
  
 **Senha**  
 Se a coluna **Status** indicar **Senha necessária**, insira a senha para a chave mestra do banco de dados.  
  
 **Atualizar**  
 Clique para atualizar a grade. Isso será útil após você inserir as senhas necessárias.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
