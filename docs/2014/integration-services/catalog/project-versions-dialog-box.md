---
title: Caixa de diálogo Versões do Projeto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isprojectprop.versions.f1
ms.assetid: a48a387c-2e70-45bc-be2e-26e57a9bb2c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 998dd194c2a056121fd6f7a404e75c7080b85aa1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439043"
---
# <a name="project-versions-dialog-box"></a>Caixa de diálogo Versões do Projeto
  Use a caixa de diálogo **Versões de Projeto** para exibir versões de um projeto e restaurar uma versão anterior.  
  
 Você também pode exibir versões anteriores na exibição [catalog.object_versions &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-object-versions-ssisdb-database) e usar o procedimento armazenado [catalog.restore_project &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database) para restaurar as versões anteriores.  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Versões de Projeto](#open_dialog)  
  
-   [Restaurar uma versão do projeto](#restore)  
  
##  <a name="open-the-project-versions-dialog-box"></a><a name="open_dialog"></a> Abrir a caixa de diálogo Versões de Projeto  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .  
  
     Ou seja, conecte-se à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **Catálogos do Integration Services** para exibir o nó **SSISDB** .  
  
4.  O nó do **SSISDB** contém uma ou mais pastas e cada uma contém um ou mais projetos. Expanda a pasta que contém o projeto ao qual você está interessado.  
  
5.  Clique com o botão direito do mouse no projeto e clique em **Versões**.  
  
 Na caixa de diálogo **Versões do Projeto** , a tabela **Versões** exibe a lista de versões do projeto que foram implantadas no servidor, com a data e a hora em que a versão foi implantada, a data e a hora em que a versão foi restaurada (se tiver sido restaurada), a descrição de versão e um identificador de versão. A versão ativa no momento é indicada com uma marca de seleção na coluna **Atual** da tabela.  
  
##  <a name="restore-a-project-version"></a><a name="restore"></a> Restaurar uma versão do projeto  
 Para restaurar uma versão anterior de um projeto, selecione a versão na tabela **Versões** e clique em **Restaurar para Versão Selecionada**. O projeto é restaurado para a versão selecionada e essa versão é indicada com uma marca de seleção na coluna **Atual** da tabela **Versões** .  
  
  
