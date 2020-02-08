---
title: 'Assistente do grupo de disponibilidade: Especificar opções do grupo de disponibilidade'
ms.description: Describes the options found on the 'Specify Availability Group Name' page of the Availability Group Wizard within SQL Server Management Studio.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.newagwizard.specifyagname.f1
- sql13.swb.adddatabasewizard.specifyagname.f1
ms.assetid: dcb6374d-becb-4c6c-b88c-5a8273f8aa38
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 63995b32f91419ef59184251299b5238d553905a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74822570"
---
# <a name="specify-availability-group-options-page-for-an-always-on-availability-group"></a>Página Especificar Opções do Grupo de Disponibilidade de um Grupo de Disponibilidade AlwaysOn
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve as opções da página **Especificar nome de grupo de disponibilidade** . Este tópico é usado pelo [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] e pelo [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
##  <a name="PageOptions"></a> Especificar opções do grupo de disponibilidade  
 **Nome do grupo de disponibilidade**  
 Especifique o nome do grupo de disponibilidade. Para um novo grupo de disponibilidade, especifique um identificador válido do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que seja exclusivo em todos os grupos de disponibilidade no WSFC (cluster de failover do Windows Server). O tamanho máximo de um nome de grupo de disponibilidade é 128 caracteres.  

 **Tipo de cluster** Em seguida, especifique o tipo de cluster. Os tipos de cluster possíveis dependem da versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e do sistema operacional. Escolha uma opção da seguinte lista:

   * **Clustering de Failover do Windows Server**
   
      Use-o quando o grupo de disponibilidade está hospedado em instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que pertencem a um cluster de failover do Windows Server para alta disponibilidade e recuperação de desastre. Aplica-se a todas as versões com suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 

   * **EXTERNAL**
      
      Use-o quando o grupo de disponibilidade está hospedado em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerenciada por uma tecnologia de cluster externa para alta disponibilidade e recuperação de desastre, por exemplo, Pacemaker no Linux. Aplica-se ao [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] e posterior.

   * **NONE**
      
      Use-o quando o grupo de disponibilidade está hospedado em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não gerenciada por uma tecnologia de cluster para balanceamento de carga e escala de leitura. Aplica-se ao [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] e posterior. 
 
   **Detecção de integridade no nível do banco de dados** Marque essa caixa para habilitar a opção (DB_FAILOVER) de detecção de integridade no nível do banco de dados para o grupo de disponibilidade. A detecção de integridade do banco de dados informa quando um banco de dados não está mais no status online e quando algo deu errado e disparará o failover automático do grupo de disponibilidade. Consulte [Opção de failover de detecção de integridade do banco de dados do AlwaysOn do SQL Server](sql-server-always-on-database-health-detection-failover-option.md).


Selecionar a página Bancos de Dados (Assistente de Novo Grupo de Disponibilidade e Assistente para Adicionar Banco de Dados)  
  
##  <a name="LaunchWiz"></a> Tarefas relacionadas  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
