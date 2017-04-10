---
title: "Exibir pacotes do Integration Services no SQL Server Management Studio (servi&#231;o SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "visualizando pacotes"
  - "conexões [Integration Services], pacotes"
ms.assetid: 783e653c-0f1f-45ed-b3ef-5ba07b019f27
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Exibir pacotes do Integration Services no SQL Server Management Studio (servi&#231;o SSIS)
    
> [!IMPORTANT]  
>  Esse tópico discute o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , um serviço do Windows para o gerenciamento de pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] dá suporte ao serviço para compatibilidade de versões anteriores com versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], você pode gerenciar objetos como pacotes no servidor do Integration Services.  
  
 Este procedimento descreve como se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e exibir uma lista dos pacotes gerenciados pelo serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
### Para se conectar ao Integration Services  
  
1.  Clique em **Iniciar**, aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**e clique em **SQL Server Management Studio**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor**, selecione **Integration Services** na lista **Tipo de servidor**, forneça um nome de servidor na caixa **Nome do servidor** e clique em **Conectar**.  
  
    > [!IMPORTANT]  
    >  Se você não consegue se conectar ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], provavelmente o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não está sendo executado. Para saber o status do serviço, clique em **Iniciar**, aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**, aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**. No painel esquerdo, clique em **Serviços do SQL Server**. No painel direito, localize o serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Inicie o serviço se ainda não estiver em execução.  
  
     [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é aberto. Por padrão, a janela do Pesquisador de Objetos é aberta e posicionada no canto inferior esquerdo do estúdio. Se o Pesquisador de Objetos não for aberto, clique em **Pesquisador de Objetos** no menu **Exibir** .  
  
### Para visualizar os pacotes gerenciados pelo serviço Integration Services  
  
1.  No Pesquisador de Objetos, expanda a pasta Pacotes Armazenados.  
  
2.  Expanda as subpastas Pacotes Armazenados para exibir os pacotes.  
  
## Consulte também  
 [Gerenciamento de pacotes &#40;Serviço SSIS&#41;](../../integration-services/service/package-management-ssis-service.md)   
 [Usar o SQL Server Management Studio](../../ssms/use-sql-server-management-studio.md)  
  
  