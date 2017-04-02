---
title: "Editor do Gerenciador de Conex&#245;es FTP | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.ftpconnectionmanager.f1"
helpviewer_keywords: 
  - "Editor do Gerenciador de Conexões FTP"
ms.assetid: 874b6585-255b-4a43-8396-bb08c3e8ac2b
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Editor do Gerenciador de Conex&#245;es FTP
  Use a caixa de diálogo **Editor do Gerenciador de Conexões FTP** para especificar as propriedades de conexão com um servidor FTP.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões de FTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 Para saber mais sobre o gerenciador de conexões FTP, consulte [Gerenciador de Conexões FTP](../../integration-services/connection-manager/ftp-connection-manager.md).  
  
## Opções  
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
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
  
  