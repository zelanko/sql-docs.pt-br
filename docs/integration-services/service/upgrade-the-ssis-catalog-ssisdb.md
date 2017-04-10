---
title: "Atualizar o Cat&#225;logo SSIS (SSISDB) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.dbupgradewizard.f1"
ms.assetid: 170c3dc9-f5bf-4599-ae56-d24a620f23e8
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Atualizar o Cat&#225;logo SSIS (SSISDB)
  Execute o Assistente de atualização do SSISDB para atualizar o banco de dados do catálogo do SSIS, SSISDB, quando o banco de dados for mais antigo que a versão atual da instância do SQL Server. Isso ocorre quando uma das condições a seguir é verdadeira.  
  
-   Você restaurou o banco de dados de uma versão anterior do SQL Server.  
  
-   Você não removeu o banco de dados de um Grupo de Disponibilidade AlwaysOn antes de atualizar a instância do SQL Server. Isso impede a atualização automática do banco de dados. Para obter mais informações, consulte [Upgrading SSISDB in an availability group](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade).  
  
 O assistente só pode atualizar o banco de dados em uma instância de servidor local.  
  
## Atualizar o Catálogo SSIS (SSISDB) executando o Assistente de Atualização do SSISDB  
  
1.  Fazer backup do banco de dados do Catálogo SSIS, SSISDB.  
  
2.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda o servidor local e expanda **Catálogos do Integration Services**.  
  
3.  Clique com o botão direito do mouse em **SSISDB** e selecione **Atualização do Banco de Dados** para iniciar o Assistente de Atualização do SSISDB.  
  
     ![Launch the SSISDB upgrade wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-1.png "Launch the SSISDB upgrade wizard")  
  
4.  Na página **Selecionar Instância** , escolha uma instância do SQL Server no servidor local.  
  
    > [!IMPORTANT]  
    >  O assistente só pode atualizar o banco de dados em uma instância de servidor local.  
  
     Marque a caixa de seleção para indicar que você fez backup do banco de dados SSISDB antes de executar o assistente.  
  
     ![Select the server in the SSISDB Upgrade Wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-2.png "Select the server in the SSISDB Upgrade Wizard")  
  
5.  Escolha **Atualizar** para atualizar o banco de dados do Catálogo SSIS.  
  
6.  Na página **Resultado** , examine os resultados.  
  
     ![Review the results in the SSISDB Upgrade Wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-3.png "Review the results in the SSISDB Upgrade Wizard")  
  
  