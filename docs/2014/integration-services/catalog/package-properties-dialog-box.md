---
title: Caixa de diálogo Propriedades do Pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageprop.general.f1
- sql12.ssis.ssms.packageproperties.f1
ms.assetid: a70acbf4-5f5c-4606-8ce4-8eb3684233de
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 573b269f361f3f4b6d8da53ab89b5b20524f6d17
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84924316"
---
# <a name="package-properties-dialog-box"></a>Caixa de diálogo Propriedades do Pacote
  Use a caixa de diálogo **Propriedades do Pacote** para exibir propriedades de pacotes individuais armazenados no servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Para obter mais informações, consulte [Servidor do Integration Services &#40;SSIS&#41;](integration-services-ssis-server-and-catalog.md).  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Propriedades do Pacote](#open_dialog)  
  
-   [Configurar as opções](#options)  
  
##  <a name="open-the-package-properties-dialog-box"></a><a name="open_dialog"></a> Abrir a caixa de diálogo Propriedades do Pacote  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o pacote para o qual você deseja exibir propriedades.  
  
5.  Clique com o botão direito do mouse no pacote e selecione **Propriedades**.  
  
##  <a name="configure-the-options"></a><a name="options"></a> Configurar as opções  
 Use a página **Geral** para exibir as propriedades do pacote selecionado.  
  
 Todas as propriedades da página **Geral** são somente leitura.  
  
 **Nome**  
 Exibe o nome do pacote.  
  
 **Identificador**  
 Lista a ID do pacote.  
  
 **Entry Point**  
 O valor de `True` indica que o pacote é iniciado diretamente. O valor de `False` indica que o pacote é iniciado por outro pacote usando a tarefa Executar Pacote. O valor padrão é `True`.  
  
 Defina essa propriedade no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para o pacote pai e os pacotes filho clicando com o botão direito do mouse no pacote em Gerenciador de Soluções e clicando em **Pacote de Ponto de Entrada**.  
  
 **Descrição**  
 Exibe a descrição opcional do pacote.  
  
  
