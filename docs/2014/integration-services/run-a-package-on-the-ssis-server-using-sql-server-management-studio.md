---
title: Executar um pacote no servidor SSIS usando SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 56dc1bf8-99d4-41dc-bdc4-f64f1ccfd688
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a598030000e5764cecc8ababa75ef2bdd8598ed
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66056374"
---
# <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>Executar um pacote no servidor SSIS usando o SQL Server Management Studio
  Depois de implantar o projeto no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , você pode executar o pacote no servidor.  
  
 Você pode usar relatórios de operações para exibir informações sobre pacotes que foram executados, ou que estão em execução no momento, no servidor. Para saber mais, confira [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md).  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>Para executar um pacote no servidor usando o SQL Server Management Studio  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e conecte-se com a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que contém o catálogo do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
2.  No Explorador de Objetos, expanda o nó **Catálogo do Integration Services** , expanda o nó **SSISDB** e navegue até o pacote contido no projeto que você implantou.  
  
3.  Clique com o botão direito do mouse no nome do pacote e selecione **Executar**.  
  
4.  Configure a execução do pacote usando as configurações nas guias **parâmetros**, **gerenciadores de conexões**e **avançado** na caixa de diálogo **executar pacote** .  
  
5.  Clique em **OK** para executar o pacote.  
  
     -ou-  
  
     Use procedimentos armazenados para executar o pacote. Clique em **Script** para gerar a instrução Transact-SQL que cria uma instância da execução e inicia uma instância da execução. A instrução inclu uma chamada para os procedimentos armazenados catalog.create_execution, catalog.set_execution_parameter_value e catalog.start_execution. Para obter mais informações sobre esses procedimentos armazenados, consulte [catalog.create_execution &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database), [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) e [catalog.start_execution &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database).  
  
  
