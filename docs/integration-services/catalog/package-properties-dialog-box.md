---
title: Caixa de diálogo Propriedades do Pacote | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageprop.general.f1
- sql13.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 906809946b22012e6a8831017fb57769fc6063b8
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298975"
---
# <a name="package-properties-dialog-box"></a>Caixa de diálogo Propriedades do Pacote

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
 **Descrição**  
 Exibe a descrição opcional do pacote.  
  
  
