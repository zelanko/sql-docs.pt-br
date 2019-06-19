---
title: Caixa de diálogo Validar | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isprojectvalidate.f1
- sql13.ssis.ssms.ispackagevalidate.f1
ms.assetid: 134e14ce-4f8d-4a20-889a-918014c841d8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 26390931bce4a2b26a4b9e2c234368b02a1e0442
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65729153"
---
# <a name="validate-dialog-box"></a>Caixa de diálogo Validar

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use a caixa de diálogo **Validar** para verificar os problemas comuns de um projeto ou pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Se houver um problema, uma mensagem será exibida na parte superior da caixa de diálogo. Caso contrário, o termo Ready aparecerá na parte superior.  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Validar](#open_dialog)  
  
-   [Definir as opções na página Geral](#general)  
  
##  <a name="open_dialog"></a> Abrir a caixa de diálogo Validar  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o projeto ou pacote que você deseja validar.  
  
5.  Clique com o botão direito do mouse no projeto ou pacote e clique em **Validar**.  
  
##  <a name="general"></a> Definir as opções na página Geral  
 **Ambiente**  
 Selecione o ambiente que você deseja usar para validar o projeto ou pacote.  
  
 **Tempo de execução de 32 bits**  
 Opte por usar um tempo de execução de 32 bits para executar um pacote.  
  
 A guia **Parâmetros** lista os valores de parâmetros usados para validar o projeto ou pacote. As opções a seguir constam na guia Parâmetros.  
  
 **Contêiner**  
 Lista o objeto que contém o parâmetro.  
  
 **Parâmetro**  
 Lista o nome dos parâmetros  
  
 **Value**  
 Lista o valor do parâmetro.  
  
 A guia **Gerenciadores de Conexões** lista os valores de propriedade dos gerenciadores de conexões usados para validar o projeto ou pacote.  
  
 As opções a seguir constam na guia **Gerenciadores de Conexões** .  
  
 **Contêiner**  
 Lista o objeto que contém o gerenciador de conexões.  
  
 **Nome**  
 Lista o nome do gerenciador de conexões.  
  
 **Nome da propriedade**  
 Lista o nome da propriedade do gerenciador de conexões.  
  
 **Value**  
 Lista o valor atribuído à propriedade do gerenciador de conexões.  
  
  
