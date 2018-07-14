---
title: Opções (página de serviços de dependência e os resultados da consulta) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.DependencyServicesGeneral
ms.assetid: dd7f6c31-7d7f-4972-854a-1419a2826dca
caps.latest.revision: 6
author: mashamsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ecc1b6d238189ca0b9c33dd97d136d3283f1ae6b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37192096"
---
# <a name="options-query-results-and-dependency-services-page"></a>Opções (página de serviços de dependência e os resultados da consulta)
  Use esta página para especificar o servidor a ser conectado para Serviços de Dependência. Os Serviços de Dependência permitem extrair informações sobre dependências entre objetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] armazenados em diferentes servidores. Exibir dependências de objeto usando o **dependências de objeto** da caixa de diálogo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
 **O que você deseja fazer?**  
  
1.  [Abrir a caixa de diálogo Opções (página de serviços de dependência/resultados de consulta)](#open_dialog)  
  
2.  [Configurar as opções](#options)  
  
##  <a name="open_dialog"></a> Abrir a caixa de diálogo Opções (página de serviços de dependência/resultados de consulta)  
  
1.  Na [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], clique em **opções** sobre o **ferramentas** menu.  
  
2.  Expanda **Resultados da Consulta** e clique em **Serviços de Dependência**.  
  
##  <a name="options"></a> Configurar as opções  
  
### <a name="options"></a>Opções  
 **Servidor de serviços de dependência**  
 Especifique o servidor em que os Serviços de Dependência estão instalados.  
  
 **Autenticação**  
 Selecione a Autenticação do Windows para fazer logon usando uma conta de usuário do Microsoft Windows ou selecione Autenticação do SQL Server.  
  
 Quando um usuário se conecta com um nome de logon e senha especificados em uma conexão não confiável, o SQL Server efetua a autenticação verificando se uma conta de logon do SQL Server foi configurada e se a senha especificada corresponde à registrada anteriormente. Se o SQL Server não localizar a conta de logon, ocorrerá uma falha na autenticação e o usuário receberá uma mensagem de erro.  
  
 **Nome de usuário**  
 Se você estiver usando a Autenticação do SQL Server, forneça um nome de usuário.  
  
 **Senha**  
 Se você estiver usando a Autenticação do SQL Server, forneça uma senha.  
  
 **Testar**  
 Clique para testar a conexão.  
  
  
