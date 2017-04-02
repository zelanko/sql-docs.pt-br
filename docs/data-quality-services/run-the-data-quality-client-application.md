---
title: "Executar o aplicativo do cliente do Data Quality | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.browseforservers.f1"
  - "sql13.dqs.connecttoserver.f1"
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
caps.latest.revision: 13
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 13
---
# Executar o aplicativo do cliente do Data Quality
  Executar [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], e fazer logon em um [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Você precisa ter concluído a instalação do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] executando o arquivo DQSInstaller.exe. Para obter mais informações, consulte [DQSInstaller.exe executar para concluir a instalação do Data Quality Server](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter uma das três funções DQS (dqs_adminstrator, dqs_kb_editor ou dqs_kb_operator) concedidas no banco de dados DQS_MAIN para que possa fazer logon no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="Run"></a> Executar o cliente Data Quality  
 Para executar [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] no computador onde ele foi instalado:  
  
1.  Clique em **Iniciar**, aponte para **todos os programas**, clique em **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**, clique em **Serviços de qualidade de dados**, e, em seguida, clique em **cliente Data Quality**.  
  
2.  No **conectar ao servidor** caixa de diálogo:  
  
    1.  Especifique o servidor ao qual você deseja conectar o aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Selecione **(LOCAL)** para se conectar ao [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] no computador local. Você também pode clicar na seta e selecione **\< network procurar mais servidores>** para se conectar a um servidor diferente (ou para se conectar ao servidor local por nome). O **Procurar servidores** caixa de diálogo será exibida. Você pode selecionar um servidor no **servidores locais** guia ou o **servidores de rede** guia.  
  
    2.  Para criptografar os dados transferidos entre [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], clique em **opções**, e, em seguida, selecione o **criptografar conexão** caixa de seleção.  
  
3.  Clique em **Conectar**.  
  
 A tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] é exibida. Para obter mais informações, consulte [dados qualidade cliente tela inicial](../data-quality-services/data-quality-client-home-screen.md).  
  
  