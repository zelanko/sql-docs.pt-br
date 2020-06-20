---
title: Opções (página resultados da consulta e serviços de dependência) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.DependencyServicesGeneral
ms.assetid: dd7f6c31-7d7f-4972-854a-1419a2826dca
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d19228fdf17788e9118367a6f0f0eb3be90cb72a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84930127"
---
# <a name="options-query-results-and-dependency-services-page"></a>Opções (página Resultados da consulta e Serviços de Dependência)
  Use esta página para especificar o servidor a ser conectado para Serviços de Dependência. Os Serviços de Dependência permitem extrair informações sobre dependências entre objetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] armazenados em diferentes servidores. Você exibe dependências de objeto usando a caixa de diálogo **dependências de objeto** no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] .  
  
 **O que você deseja fazer?**  
  
1.  [Abrir a caixa de diálogo de opções (página de resultados da consulta/Serviços de Dependência)](#open_dialog)  
  
2.  [Configurar as opções](#options)  
  
##  <a name="open-the-options-query-resultsdependency-services-page-dialog-box"></a><a name="open_dialog"></a>Abrir a caixa de diálogo Opções (página resultados da consulta/serviços de dependência)  
  
1.  No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] , clique em **Opções** no menu **ferramentas** .  
  
2.  Expanda **Resultados da Consulta** e clique em **Serviços de Dependência**.  
  
##  <a name="configure-the-options"></a><a name="options"></a>Configurar as opções  
  
### <a name="options"></a>Opções  
 **Servidor dos Serviços de Dependência**  
 Especifique o servidor em que os Serviços de Dependência estão instalados.  
  
 **Autenticação**  
 Selecione a Autenticação do Windows para fazer logon usando uma conta de usuário do Microsoft Windows ou selecione Autenticação do SQL Server.  
  
 Quando um usuário se conecta com um nome de logon e senha especificados em uma conexão não confiável, o SQL Server efetua a autenticação verificando se uma conta de logon do SQL Server foi configurada e se a senha especificada corresponde à registrada anteriormente. Se o SQL Server não localizar a conta de logon, ocorrerá uma falha na autenticação e o usuário receberá uma mensagem de erro.  
  
 **Nome de usuário**  
 Se você estiver usando a Autenticação do SQL Server, forneça um nome de usuário.  
  
 **Senha**  
 Se você estiver usando a Autenticação do SQL Server, forneça uma senha.  
  
 **Teste**  
 Clique para testar a conexão.