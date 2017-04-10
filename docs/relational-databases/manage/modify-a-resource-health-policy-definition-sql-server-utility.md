---
title: "Modificar uma defini&#231;&#227;o de pol&#237;tica de integridade de recursos (Utilit&#225;rio do SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.SWB.UE.UTILITY.ADMINISTRATION.F1"
ms.assetid: 27bec0b6-92e9-448e-8c70-fe36802cf128
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Modificar uma defini&#231;&#227;o de pol&#237;tica de integridade de recursos (Utilit&#225;rio do SQL Server)
  Este tópico descreve como modificar uma definição de política de integridade de recursos no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Antes de modificar uma política de utilização de recursos no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve criar um UCP (ponto de controle de utilitário). Para obter mais informações, consulte [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As políticas de utilização de recursos do Utilitário podem ser configuradas para aplicativos da camada de dados e instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As políticas de utilização de recursos podem ser definidas globalmente para todos os aplicativos da camada de dados e instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou podem ser definidas individualmente para cada aplicativo da camada de dados e para cada instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Também é possível implementar políticas globais e fazer com que os aplicativos da camada de dados individuais ou as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sejam configuradas com suas próprias definições de políticas.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Modifique políticas de utilização de recursos globais em um Utilitário do SQL Server.  
  
1.  Conecte-se ao UCP no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  No painel de navegação do Gerenciador do Utilitário, clique em **Administração de Utilitário** para exibir ou modificar políticas de monitoramento globais e clique na guia **Política** no painel de conteúdo do Gerenciador do Utilitário.  
  
3.  No painel de conteúdo do Gerenciador do Utilitário, selecione **Definir políticas globais de monitoramento da camada de dados** ou **Definir políticas globais de monitoramento de instância gerenciada** clicando na seta ou na descrição da política.  
  
4.  Use os controles no lado direito das descrições das políticas para definir os limites de subutilização ou superutilização da política.  
  
5.  Use os botões **Aplicar**, **Descartar**ou **Restaurar Padrões** conforme necessário. A alteração da política pode levar até 15 minutos para ser propagada para os detalhes do painel e exibição de lista do utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
6.  Para atualizar dados, clique com o botão direito do mouse no nó **Administração do Utilitário** no painel de navegação do Gerenciador do Utilitário e selecione **Atualizar**.  
  
#### Modificar definições de políticas de integridade de recursos para um aplicativo da camada de dados individual ou uma instância gerenciada individual de SQL Server em um Utilitário do SQL Server  
  
1.  Conecte-se ao UCP no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  No painel de navegação do Gerenciador do Utilitário, clique em **Aplicativos da Camada de Dados Implantados** ou clique em **Instâncias Gerenciadas** para exibir ou modificar políticas de monitoramento para uma instância gerenciada ou aplicativo da camada de dados individual.  
  
3.  Na exibição de lista do painel de conteúdo do Gerenciador do Utilitário, clique no aplicativo da camada de dados ou no nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cujas políticas você deseja modificar e clique na guia **Detalhes da Política**.  
  
4.  Selecione a política a ser exibida ou modificada clicando na seta ou na descrição da política. Por padrão, as políticas globais são selecionadas.  
  
5.  Selecione o botão de opção **Substituir a política global** para substituir políticas globais e implementar uma definição de política individual para o aplicativo da camada de dados especificado.  
  
6.  Use os controles no lado direito da descrição da política para definir os limites de subutilização ou superutilização da política.  
  
7.  Use os botões **Aplicar**, **Descartar**ou **Restaurar Padrões** conforme necessário. A alteração da política pode levar até 15 minutos para ser propagada para os detalhes do painel e exibição de lista do utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
8.  Para atualizar dados, clique com o botão direito do mouse no nó **Aplicativos da Camada de Dados Implantados** no painel de navegação do Gerenciador do Utilitário e selecione **Atualizar**.  
  
## Consulte também  
 [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Exibir resultados da política de integridade de recursos &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)  
  
  