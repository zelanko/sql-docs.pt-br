---
title: Editor do Gerenciador de Conexão de FTP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftpconnectionmanager.f1
helpviewer_keywords:
- FTP Connection Manager Editor
ms.assetid: 874b6585-255b-4a43-8396-bb08c3e8ac2b
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 79f2d2c03d2403042de7f1ca0aeed3db15c93efc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48189136"
---
# <a name="ftp-connection-manager-editor"></a>Editor do Gerenciador de Conexões FTP
  Use a caixa de diálogo **Editor do Gerenciador de Conexões FTP** para especificar as propriedades de conexão com um servidor FTP.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões de FTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 Para saber mais sobre o gerenciador de conexões FTP, consulte [Gerenciador de Conexões FTP](connection-manager/ftp-connection-manager.md).  
  
## <a name="options"></a>Opções  
 **Nome do servidor**  
 Forneça o nome do servidor FTP.  
  
 **Porta do servidor**  
 Especifique o número da porta no servidor FTP a ser usada na conexão. O valor padrão dessa propriedade é **21**.  
  
 **Nome de usuário**  
 Forneça um nome de usuário para acessar o servidor FTP. O valor padrão dessa propriedade é **anonymous**.  
  
 **Senha**  
 Forneça uma senha para acessar o servidor FTP.  
  
 **Tempo limite (em segundos)**  
 Especifique o número de segundos que a tarefa terá antes de exceder o tempo limite. O valor **0** indica um tempo infinito. O valor padrão dessa propriedade é **60**.  
  
 **Usar modo passivo**  
 Especifique se o servidor ou o cliente inicia a conexão. No modo ativo, o servidor inicia a conexão e, no modo passivo, o cliente ativa a conexão. O valor padrão dessa propriedade é **active mode**.  
  
 **Novas tentativas**  
 Especifique o número de vezes que a tarefa tenta fazer uma conexão. Um valor de **0** indica que não há limite ao número de tentativas.  
  
 **Tamanho da parte (em KB)**  
 Forneça um tamanho de parte em kilobytes para transmissão de dados.  
  
 **Testar Conexão**  
 Depois de configurar o Gerenciador de Conexões FTP, confirme se a conexão é viável clicando em **Testar Conexão**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
