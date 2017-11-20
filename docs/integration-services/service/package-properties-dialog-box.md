---
title: "Caixa de diálogo Propriedades do pacote | Microsoft Docs"
ms.custom: 
ms.date: 08/26/2016
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: service
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.ssms.ispackageprop.general.f1
- sql13.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 2a3d348ee8bfe53c20d66b5dc39f96b4a4be635c
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="package-properties-dialog-box"></a>Caixa de diálogo Propriedades do Pacote
  Use a caixa de diálogo **Propriedades do Pacote** para exibir propriedades de pacotes individuais armazenados no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Para obter mais informações, consulte [Servidor do Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md).  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Propriedades do Pacote](#open_dialog)  
  
-   [Configurar as opções](#options)  
  
##  <a name="open_dialog"></a> Abrir a caixa de diálogo Propriedades do Pacote  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o pacote para o qual você deseja exibir propriedades.  
  
5.  Clique com o botão direito do mouse no pacote e selecione **Propriedades**.  
  
##  <a name="options"></a> Configurar as opções  
 Use a página **Geral** para exibir as propriedades do pacote selecionado.  
  
 Todas as propriedades da página **Geral** são somente leitura.  
  
 **Nome**  
 Exibe o nome do pacote.  
  
 **Identificador**  
 Lista a ID do pacote.  
  
 **Entry Point**  
 O valor de **True** indica que o pacote é iniciado diretamente. O valor de **False** indica que o pacote é iniciado por outro pacote usando a tarefa Executar Pacote. O valor padrão é **True**.  
  
 Defina essa propriedade no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para o pacote pai e os pacotes filho clicando com o botão direito do mouse no pacote em Gerenciador de Soluções e clicando em **Pacote de Ponto de Entrada**.  
  
 **Description**  
 Exibe a descrição opcional do pacote.  
  
  

