---
title: Página Selecionar Bancos de Dados (Assistente de Novo Grupo de Disponibilidade e Assistente para Adicionar Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.adddatabasewizard.selectdatabases.f1
- sql13.swb.newagwizard.selectdatabases.f1
ms.assetid: 929c5e15-d087-438d-b1f2-aa97c5f8bff8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 04836a29531c1eaab61277891e22e31b669d9ffd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68014193"
---
# <a name="select-databases-page-new-availability-group-wizard-and-add-database-wizard"></a>Selecionar a página Bancos de Dados (Assistente de Novo Grupo de Disponibilidade e Assistente para Adicionar Banco de Dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve as opções da página **Especificar Bancos de Dados** . Este tópico aplica-se ao [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] e ao [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
##  <a name="PageOptions"></a> Selecionar opções de bancos de dados  
 A grade **Bancos de dados de usuário nesta instância do SQL Server** lista todos os bancos de dados de usuário locais. As colunas são apresentadas assim:  
  
 **Nome**  
 Exibe o nome do banco de dados de usuário local.  

 **Tamanho**  
 Exibe o tamanho do banco de dados, se o tamanho estiver disponível para o assistente.  
  
 **Status**  
 Exibe um hiperlink cujo texto indica se um determinado banco de dados atende aos pré-requisitos para ser adicionado a um grupo de disponibilidade. Se o status for "**Atende pré-requisitos**" você poderá adicionar o banco de dados ao grupo de disponibilidade. Se um banco de dados não atender a todos os pré-requisitos, o hiperlink **Status** fornecerá uma breve explicação de por que o banco de dados não está qualificado. Para obter mais informações, clique no hiperlink.  
  
 Você pode deixar o assistente na página **Selecionar Banco de Dados** enquanto executa ações em um banco de dados para atender a um pré-requisito. Ao retornar à página **Selecionar Bancos de Dados** , clique em **Atualizar** para atualizar a grade.  
  
 **Senha**  
 Se o banco de dados contiver uma chave mestra de banco de dados, digite a senha da chave mestra do banco de dados.  
  
 **Atualizar**  
 Clique para atualizar a grade. Isso é útil depois que você executa uma ação em um banco de dados para atender a um pré-requisito.  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Pré-requisitos, restrições e recomendações para grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
