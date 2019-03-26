---
title: Gerenciador de conexões do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 01/25/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 24d68966f3a4ce719b2d22c10df0d1b265b85c93
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275826"
---
# <a name="analysis-services-connection-manager"></a>Gerenciador de conexões do Analysis Services
  Um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] habilita um pacote para se conectar a um servidor que executa um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que fornece acesso a dados de cubos e dimensões. Você só pode se conectar a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] enquanto estiver desenvolvendo pacotes no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Em tempo de execução, os pacotes são conectados ao servidor e ao banco de dados em que foi implantado o projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 As tarefas Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e os destinos, como o destino Treinamento do Modelo de Mineração de Dados, usam um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Para obter mais informações sobre bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Bancos de dados de modelo multidimensional &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md).  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Configuração do Gerenciador de Conexões do Analysis Services  
 Quando você adiciona um gerenciador de conexões [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a um pacote, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões resolvido como uma conexão [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em tempo de execução, define as propriedades do gerenciador de conexões e o adiciona à coleção **Conexões** no pacote. A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **MSOLAP100**.  
  
 Você pode configurar um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] das seguintes maneiras:  
  
-   Forneça uma cadeia de conexão configurada para atender aos requisitos do provedor Microsoft OLE Provider para Analysis Services.  
  
-   Especifique uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que deseja conectar.  
  
-   Se estiver se conectando a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], especifique o modo de autenticação.  

> [!NOTE]    
>  Caso use o SSIS no ADF (Azure Data Factory) e queira se conectar à instância do AAS (Azure Analysis Services), você não poderá usar uma conta com a MFA (Autenticação Multifator) habilitada, mas deverá usar uma conta que não exija nenhuma interatividade/MFA ou uma entidade de serviço. Para usar a última opção, veja [aqui](https://docs.microsoft.com/azure/analysis-services/analysis-services-service-principal) para criar uma e atribuir a função de administrador do servidor a ela, selecione **usar um determinado nome de usuário e senha** para fazer logon no servidor no seu Gerenciador de conexão e, por fim, insira `User name: app:YourApplicationID` e `Password: YourAuthorizationKey`.
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique em um dos seguintes tópicos:  
  
-   [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](../../integration-services/connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
  
