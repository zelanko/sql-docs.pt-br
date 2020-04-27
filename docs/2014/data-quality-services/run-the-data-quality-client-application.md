---
title: Executar o aplicativo Data Quality Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.browseforservers.f1
- sql12.dqs.connecttoserver.f1
ms.assetid: 0b2aa202-7ab2-4c9d-b0f1-802588053a1e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bbb790fc5067d1544cd4b3d9d6e90b34be8e2b77
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65484147"
---
# <a name="run-the-data-quality-client-application"></a>Executar o aplicativo do cliente do Data Quality
  É possível usar o [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) executando o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] e fazendo logon em um [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
 Você precisa ter concluído a instalação do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] executando o arquivo DQSInstaller.exe. Para obter mais informações, consulte [Executar o DQSInstaller.exe para concluir a instalação do Data Quality Server](install-windows/run-dqsinstaller-exe-to-complete-data-quality-server-installation.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Você deve ter uma das três funções DQS (dqs_adminstrator, dqs_kb_editor ou dqs_kb_operator) concedidas no banco de dados DQS_MAIN para que possa fazer logon no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
##  <a name="run-data-quality-client"></a><a name="Run"></a>Executar Data Quality Client  
 Para executar o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] no computador onde ele foi instalado, faça o seguinte:  
  
1.  Clique em **Iniciar**, aponte para **Todos os Programas**, clique em **[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**, clique em **Data Quality Services**e clique em **Cliente Data Quality**.  
  
2.  Na caixa de diálogo **Conectar ao Servidor** :  
  
    1.  Especifique o servidor ao qual você deseja conectar o aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Selecione **(LOCAL)** para conectar ao [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] no computador local. Você também pode clicar na seta para baixo e selecionar ** \<procurar mais servidores na rede>** para se conectar a um servidor diferente (ou para se conectar ao servidor local por nome). A caixa de diálogo **Procurar Servidores** será exibida. Você pode selecionar um servidor na guia **Servidores Locais** ou na guia **Servidores de Rede** .  
  
    2.  Se você deseja criptografar a transferência de dados entre o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] e o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], clique em **Opções** e marque a caixa de seleção **Criptografar Conexão**.  
  
3.  Clique em **Conectar**.  
  
 A tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] é exibida. Para obter mais informações, consulte [Data Quality Services Concepts](../../2014/data-quality-services/data-quality-client-home-screen.md).  
  
  
