---
title: Caixa de diálogo Definir Valor do Parâmetro | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ce9c2201-4e9a-4495-948f-b68deeaa7955
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 50bdca11c1e56e0e35c68efe79986c621da94825
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439023"
---
# <a name="set-parameter-value-dialog-box"></a>Caixa de diálogo Definir Valor do Parâmetro
  Use a caixa de diálogo **Definir Valor do Parâmetro** para definir valores de parâmetros e propriedades do gerenciador de conexões para projetos e pacotes.  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Definir Valor do Parâmetro](#open_dialog)  
  
-   [Configurar as opções](#option)  
  
##  <a name="open-the-set-parameter-value-dialog-box"></a><a name="open_dialog"></a> Abrir a caixa de diálogo Definir Valor do Parâmetro  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Clique com o botão direito do mouse em um pacote ou projeto, clique em **Configurar**e clique no botão de reticências na guia **Parâmetros** ou na guia **Gerenciadores de Conexões** .  
  
##  <a name="configure-the-options"></a><a name="option"></a> Configurar as opções  
 **Parâmetro**  
 Lista o nome do parâmetro.  
  
 **Tipo**  
 Lista o tipo de dados do valor do parâmetro.  
  
 **Descrição**  
 Mostra uma descrição opcional para o parâmetro.  
  
 **Editar valor**  
 Selecione essa opção para editar o valor do parâmetro.  
  
 **Usar valor padrão do pacote**  
 Selecione essa opção para usar o valor de parâmetro padrão armazenado no pacote.  
  
 **Usar variável de ambiente**  
 Selecione essa opção para usar um valor de variável armazenado no ambiente, que é referenciado pelo projeto ou pacote. Para adicionar uma referência de ambiente a um projeto ou pacote, use a caixa de diálogo **Configurar** . Para obter mais informações, consulte [Configure Dialog Box](configure-dialog-box.md).  
  
  
