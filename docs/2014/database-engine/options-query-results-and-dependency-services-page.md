---
title: Opções (resultados da consulta e página serviços de dependência) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.DependencyServicesGeneral
ms.assetid: dd7f6c31-7d7f-4972-854a-1419a2826dca
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 6f5cabf63916602f3a269b24b1e43e24e42f9082
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007105"
---
# <a name="options-query-results-and-dependency-services-page"></a>Opções (resultados da consulta e página serviços de dependência)
  Use esta página para especificar o servidor a ser conectado para Serviços de Dependência. Os Serviços de Dependência permitem extrair informações sobre dependências entre objetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] armazenados em diferentes servidores. Exibir dependências de objeto usando o **dependências de objeto** da caixa de diálogo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
 **O que você deseja fazer?**  
  
1.  [Abrir a caixa de diálogo Opções (página de serviços de dependência/resultados de consulta)](#open_dialog)  
  
2.  [Configurar as opções](#options)  
  
##  <a name="open_dialog"></a> Abrir a caixa de diálogo Opções (página de serviços de dependência/resultados de consulta)  
  
1.  Em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], clique em **opções** no **ferramentas** menu.  
  
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
  
  