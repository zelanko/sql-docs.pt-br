---
title: "Editor da Tarefa FTP (p&#225;gina Transfer&#234;ncia de Arquivos) | Microsoft Docs"
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
  - "sql13.dts.designer.ftptask.filetransfer.f1"
helpviewer_keywords: 
  - "Editor da Tarefa FTP"
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Editor da Tarefa FTP (p&#225;gina Transfer&#234;ncia de Arquivos)
  Use a página **Transferência de Arquivos** da caixa de diálogo **Editor da Tarefa FTP** para configurar a operação FTP executada pela tarefa.  
  
 Para obter informações sobre essa tarefa, consulte [Tarefa FTP](../../integration-services/control-flow/ftp-task.md).  
  
## Opções  
 **IsRemotePathVariable**  
 Indique se o caminho remoto deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Verdadeiro**|O caminho de destino é armazenado em uma variável. Ao selecionar esse valor, a opção dinâmica **RemoteVariable** será exibida.|  
|**Falso**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **RemotePath** será exibida.|  
  
 **OverwriteFileAtDestination**  
 Especifique se um arquivo no destino pode ser substituído.  
  
 **IsLocalPathVariable**  
 Indique se o caminho local deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Verdadeiro**|O caminho de destino é armazenado em uma variável. Ao selecionar esse valor, a opção dinâmica **LocalVariable** será exibida.|  
|**Falso**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **LocalPath** será exibida.|  
  
 **Operação**  
 Selecione a operação FTP a executar. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Value|Description|  
|-----------|-----------------|  
|**Enviar arquivos**|Enviar arquivos. Ao selecionar esse valor, as opções dinâmicas **LocalVariable**, **LocalPathRemoteVariable** e **RemotePath** serão exibidas.|  
|**Receber arquivos**|Receber arquivos. Ao selecionar esse valor, as opções dinâmicas **LocalVariable**, **LocalPathRemoteVariable** e **RemotePath** serão exibidas.|  
|**Criar diretório local**|Criar um diretório local. Ao selecionar esse valor, as opções dinâmicas **LocalVariable** e **LocalPath** serão exibidas.|  
|**Criar diretório remoto**|Criar um diretório remoto. Ao selecionar esse valor, as opções dinâmicas **RemoteVariable** e **RemotelPath** serão exibidas.|  
|**Remover diretório local**|Remover diretório local. Ao selecionar esse valor, as opções dinâmicas **LocalVariable** e **LocalPath** serão exibidas.|  
|**Remover diretório remoto**|Remover um diretório remoto. Ao selecionar esse valor, as opções dinâmicas **RemoteVariable** e **RemotePath** serão exibidas.|  
|**Excluir arquivos locais**|Excluir arquivos locais. Ao selecionar esse valor, as opções dinâmicas **LocalVariable** e **LocalPath** serão exibidas.|  
|**Excluir arquivos remotos**|Excluir arquivos remotos. Ao selecionar esse valor, as opções dinâmicas **RemoteVariable** e **RemotePath** serão exibidas.|  
  
 **IsTransferASCII**  
 Indique se os arquivos transferidos para e do servidor FTP remoto devem ser transferidos em modo ASCII.  
  
## Opções dinâmicas de IsRemotePathVariable  
  
### IsRemotePathVariable = True  
 **RemoteVariable**  
 Selecione uma variável definida pelo usuário existente ou clique em \<**Nova variável...**> para criar uma variável definida pelo usuário.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), Adicionar variável  
  
### IsRemotePathVariable = False  
 **RemotePath**  
 Selecione um gerenciador de conexões de FTP existente ou clique em \<**Nova conexão…**> para criar um gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager.md), [Editor do Gerenciador de Conexões de FTP](../../integration-services/connection-manager/ftp-connection-manager-editor.md)  
  
## Opções dinâmicas de IsLocalPathVariable  
  
### IsLocalPathVariable = True  
 **LocalVariable**  
 Selecione uma variável definida pelo usuário existente ou clique em \<**Nova variável...**> para criar uma variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), Adicionar variável  
  
### IsLocalPathVariable = False  
 **LocalPath**  
 Selecione um gerenciador de conexões de arquivos existente ou clique em \<**Nova conexão…**> para criar um gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de Conexões de Arquivos Simples](../../integration-services/connection-manager/flat-file-connection-manager.md), [Editor do Gerenciador de Conexões de Arquivos Simples](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa FTP &#40;página Geral&#41;](../../integration-services/control-flow/ftp-task-editor-general-page.md)   
 [Página Expressões](../../integration-services/expressions/expressions-page.md)  
  
  