---
title: Caixa de diálogo Procurar Todas as Entidades de Segurança | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.browseprincipals.f1
ms.assetid: f11d2c5e-ee05-45f3-8dc2-0feb99b2f76f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 46d6fd5d4ecd821a3ccfeb35679e8fa7bab6104e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771712"
---
# <a name="browse-all-principals-dialog-box"></a>Caixa de diálogo Procurar Todas as Entidades de Segurança
  Use a caixa de diálogo **Procurar Todas as Entidades de Segurança** para selecionar uma entidade de segurança de banco de dados para alterar as permissões da entidade de segurança no projeto selecionado ou em todos os projetos contidos em uma pasta selecionada.  
  
 **O que você deseja fazer?**  
  
-   [Caixa de diálogo Abrir Todas as Entidades de Segurança](#open_dialog)  
  
-   [Configurar as opções](#options)  
  
##  <a name="open_dialog"></a> Caixa de diálogo Abrir Todas as Entidades de Segurança  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o catálogo SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Para alteraras permissões da entidade de segurança em todos os projetos contidos em uma pasta selecionada, clique com o botão direito do mouse na pasta e clique em **Propriedades**.  
  
     Para alteraras permissões da entidade de segurança em um projeto selecionado, expanda a pasta que contém o projeto, clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
5.  Selecione a página **Permissões** e clique em **Procurar**.  
  
##  <a name="options"></a> Configurar as opções  
 Esta página exibe as entidades de segurança da exibição do catálogo, sys.database_principals, do banco de dados do SSISDB.  
  
 Ao serem selecionadas, as entidades de segurança serão adicionadas à lista **Logons ou funções** na página **Permissões** da caixa de diálogo pai quando você clicar em **OK** e fechar a caixa de diálogo **Procurar Todas as Entidades de Segurança** . Depois de adicionar entidades de segurança à lista **Logons ou funções** , você poderá alterar as permissões no projeto selecionado.  
  
 **Seleção de coluna**  
 Selecione para adicionar a entidade de segurança à lista **Logons ou funções** na página **Permissões** da caixa de diálogo pai.  
  
 **Coluna de ícone**  
 Um ícone que corresponde ao **Tipo** da entidade de segurança.  
  
 **Nome**  
 O nome da entidade de segurança.  
  
 **Tipo**  
 O tipo da entidade de segurança. Os tipos comuns são:  
  
-   Usuário do SQL  
  
-   Usuário do Windows  
  
-   Função de banco de dados  
  
  
