---
title: Caixa de diálogo Configurar | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.configure.f1
- sql13.SSIS.SSMS.ISPROJECTPROP.REFERENCES.F1
- sql13.SSIS.SSMS.ISPROJECTPROP.PARAMETERS.F1
ms.assetid: 10183c8d-b1be-420f-972a-96ea97d4f4d8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c1089176ed6b47ab7001f0a505b7d475bf1241c4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662384"
---
# <a name="configure-dialog-box"></a>Caixa de diálogo Configurar
  Use a caixa de diálogo **Configurar** para configurar parâmetros, gerenciadores de conexões e referências a ambientes para projetos e pacotes.  
  
 **O que você deseja fazer?**  
  
-   [Abrir a caixa de diálogo Configurar](#open_dialog)  
  
-   [Definir as opções na página Parâmetros](#parameter)  
  
-   [Definir as opções na página Referências](#references)  
  
##  <a name="open_dialog"></a> Abrir a caixa de diálogo Configurar  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o pacote ou projeto que você deseja configurar.  
  
5.  Clique com o botão direito do mouse no pacote ou projeto e clique em **Configurar**.  
  
##  <a name="parameter"></a> Definir as opções na página Parâmetros  
 Use a página **Parâmetros** para exibir nomes e valores de parâmetro, e para modificar os valores.  
  
 Selecione o escopo dos parâmetros exibidos nas guias **Parâmetros** e **Gerenciadores de Conexões** , na lista suspensa **Escopo** .  
  
 Esta é uma lista das opções na guia **Parâmetros** .  
  
 **Contêiner**  
 Lista o objeto que contém o parâmetro.  
  
 **Nome**  
 Lista o nome do parâmetro.  
  
 **Value**  
 Lista o valor do parâmetro. Clique no botão de reticências para alterar o valor na caixa de diálogo **Definir Valor do Parâmetro** .  
  
 Esta é uma lista das opções na guia **Gerenciadores de Conexões** . Use essa guia para alterar valores de propriedades do gerenciador de conexões. Os parâmetros são gerados automaticamente no servidor do SSIS para as propriedades.  
  
 **Contêiner**  
 Lista o objeto que contém o gerenciador de conexões.  
  
 **Nome**  
 Lista o nome do gerenciador de conexões.  
  
 **Nome da propriedade**  
 Lista o nome da propriedade do gerenciador de conexões.  
  
 **Value**  
 Lista o valor atribuído à propriedade do gerenciador de conexões. Clique no botão de reticências para alterar o valor na caixa de diálogo **Definir Valor do Parâmetro** . Você pode inserir um valor literal, mapear uma variável de ambiente que contém o valor a ser usado, ou usar o valor padrão do pacote.  
  
##  <a name="references"></a> Definir as opções na página Referências  
 Use a página **Referências** para adicionar e remover referências a ambientes, e para acessar propriedades de ambiente.  
  
 Um ambiente especificar valores de tempo de execução para pacotes contidos nos projetos que você implantou no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 **Ambiente**  
 Lista o ambiente.  
  
 **Pasta de Ambiente**  
 Lista a pasta que contém o ambiente.  
  
 **Abrir**  
 Clique para abrir a caixa de diálogo **Propriedades do Ambiente** .  
  
 **Adicionar**  
 Clique para adicionar uma referência a um ambiente. Na caixa de diálogo **Procurar Ambientes** , clique em um ambiente e clique em **OK**.  
  
 Você pode selecionar um ambiente contido em qualquer pasta de projeto no nó **SSISDB** .  
  
 **Remover**  
 Clique em um ambiente listado na área **Referências** e clique em **Remover**.  
  
  
