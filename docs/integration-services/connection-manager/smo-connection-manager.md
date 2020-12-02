---
description: gerenciador de conexões SMO
title: Gerenciador de Conexões SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.smoconnection.f1
helpviewer_keywords:
- connections [Integration Services], SMO
- SMO connection manager
- connection managers [Integration Services], SMO
ms.assetid: d273f1fb-a6a8-4f2f-a5ff-55c2e3de4723
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 23a54cf3d07772276dbdf21dd7bf752a35121097
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91719299"
---
# <a name="smo-connection-manager"></a>gerenciador de conexões SMO

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Um gerenciador de conexões SMO habilita um pacote para conexão a um servidor do SQL Management Object (SMO). As tarefas de transferência que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usam um gerenciador de conexões do SMO. Por exemplo, a tarefa Transferir Logons que transfere os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um gerenciador de conexões do SMO.  
  
 Quando você adiciona um gerenciador de conexões SMO a um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cria um gerenciador de conexões que disponibilizará uma conexão do SMO no momento da execução, define as propriedades do gerenciador de conexões e adiciona o gerenciador de conexões à coleção do **Connections** no pacote. A propriedade **ConnectionManagerType** do gerenciador de conexões está definida como **SMOServer**.  
  
 Você pode configurar um gerenciador de conexões SMO das seguintes maneiras:  
  
-   Especifique o nome de um servidor no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está instalado.  
  
-   Selecione o modo de autenticação para a conexão com o servidor.  
  
## <a name="configuration-of-the-smo-connection-manager"></a>Configuração do gerenciador de conexões SMO  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Editor do Gerenciador de Conexões do SMO]().  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="smo-connection-manager-editor"></a>Editor do Gerenciador de Conexões SMO
  Use o **Editor do Gerenciador de Conexões SMO** para configurar uma conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uso das várias tarefas que transferem objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para saber mais sobre o gerenciador de conexões SMO, consulte [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md).  
  
### <a name="options"></a>Opções  
 **Nome do servidor**  
 Digite o nome da instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou selecione o nome do servidor da lista.  
  
 **Atualizar**  
 Atualize a lista de instâncias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponíveis que podem ser detectadas na rede.  
  
 **Usar Autenticação do Windows**  
 Use a Autenticação do Windows para conectar-se à instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selecionada.  
  
 **Usar Autenticação do SQL Server**  
 Use a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectar-se à instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selecionada.  
  
 **Nome de usuário**  
 Se você selecionou a autenticação de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , digite o nome de usuário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Senha**  
 Se você selecionou a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , digite a senha.  
  
 **Testar Conexão**  
 Teste a conexão como foi configurada.  
  
## <a name="see-also"></a>Consulte Também  
 [Conexões do SSIS &#40;Integration Services&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
