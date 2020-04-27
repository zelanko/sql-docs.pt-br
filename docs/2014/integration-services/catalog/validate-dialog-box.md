---
title: Caixa de diálogo Validar | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackagevalidate.f1
- sql12.ssis.ssms.isprojectvalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8380b3ff1502088e0131b182149e90e31d2be42c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771643"
---
# <a name="validate-dialog-box"></a>Caixa de diálogo Validar
  Use a caixa de diálogo **Validar** para verificar os problemas comuns de um projeto ou pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Se houver um problema, uma mensagem será exibida na parte superior da caixa de diálogo. Caso contrário, o termo Ready aparecerá na parte superior.  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Validar](#open_dialog)  
  
-   [Definir as opções na página Geral](#general)  
  
##  <a name="open-the-validate-dialog-box"></a><a name="open_dialog"></a> Abrir a caixa de diálogo Validar  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o projeto ou pacote que você deseja validar.  
  
5.  Clique com o botão direito do mouse no projeto ou pacote e clique em **Validar**.  
  
##  <a name="set-the-options-on-the-general-page"></a><a name="general"></a> Definir as opções na página Geral  
 **Ambiente**  
 Selecione o ambiente que você deseja usar para validar o projeto ou pacote.  
  
 **runtime de 32 bits**  
 Opte por usar um runtime de 32 bits para executar um pacote.  
  
 A guia **Parâmetros** lista os valores de parâmetros usados para validar o projeto ou pacote. As opções a seguir constam na guia Parâmetros.  
  
 **Contêiner**  
 Lista o objeto que contém o parâmetro.  
  
 **Parâmetro**  
 Lista o nome dos parâmetros  
  
 **Valor**  
 Lista o valor do parâmetro.  
  
 A guia **Gerenciadores de Conexões** lista os valores de propriedade dos gerenciadores de conexões usados para validar o projeto ou pacote.  
  
 As opções a seguir constam na guia **Gerenciadores de Conexões** .  
  
 **Contêiner**  
 Lista o objeto que contém o gerenciador de conexões.  
  
 **Nome**  
 Lista o nome do gerenciador de conexões.  
  
 **Nome da propriedade**  
 Lista o nome da propriedade do gerenciador de conexões.  
  
 **Valor**  
 Lista o valor atribuído à propriedade do gerenciador de conexões.  
  
  
