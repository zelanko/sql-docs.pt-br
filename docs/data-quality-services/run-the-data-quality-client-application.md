---
title: Executar o aplicativo Data Quality Client | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.browseforservers.f1
- sql13.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: add70b6a98a0246b2ad8ae8743ca57763e157f89
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56011509"
---
# <a name="run-the-data-quality-client-application"></a>Executar o aplicativo do cliente do Data Quality

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Executar [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], e fazer logon em um [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Prerequisites"></a> Pré-requisitos  
 Você precisa ter concluído a instalação do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] executando o arquivo DQSInstaller.exe. Para obter mais informações, consulte [Executar o DQSInstaller.exe para concluir a instalação do Data Quality Server](../data-quality-services/install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Você deve ter uma das três funções DQS (dqs_adminstrator, dqs_kb_editor ou dqs_kb_operator) concedidas no banco de dados DQS_MAIN para que possa fazer logon no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="Run"></a> Executar o cliente Data Quality  
 Para executar o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] no computador em que ele foi instalado:  
  
1.  Clique em **Iniciar**, aponte para **Todos os Programas**, clique em **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**, clique em **Data Quality Services**e clique em **Cliente Data Quality**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** :  
  
    1.  Especifique o servidor ao qual você deseja conectar o aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Selecione **(LOCAL)** para conectar ao [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] no computador local. Também clique na seta para baixo e selecione **\<Procurar mais servidores na rede>** para se conectar a outro servidor (ou se conectar ao servidor local pelo nome). A caixa de diálogo **Procurar Servidores** será exibida. Você pode selecionar um servidor na guia **Servidores Locais** ou na guia **Servidores de Rede** .  
  
    2.  Para criptografar a transferência de dados entre o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], clique em **Opções**e marque a caixa de seleção **Criptografar Conexão** .  
  
3.  Clique em **Conectar**.  
  
 A tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] é exibida. Para obter mais informações, consulte [Data Quality Services Concepts](../data-quality-services/data-quality-client-home-screen.md).  
  
  
