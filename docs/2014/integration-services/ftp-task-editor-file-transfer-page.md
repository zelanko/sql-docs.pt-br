---
title: Editor da tarefa FTP (página transferência de arquivos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.filetransfer.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 37e52220-feb2-474c-ad88-fa1b1059acd4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9386070902022e29ba191f24eb8fbfb10ed92b9a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058441"
---
# <a name="ftp-task-editor-file-transfer-page"></a>Editor da Tarefa FTP (página Transferência de Arquivos)
  Use a página **Transferência de Arquivos** da caixa de diálogo **Editor da Tarefa FTP** para configurar a operação FTP executada pela tarefa.  
  
 Para obter informações sobre essa tarefa, consulte [Tarefa FTP](control-flow/ftp-task.md).  
  
## <a name="options"></a>Opções  
 **IsRemotePathVariable**  
 Indique se o caminho remoto deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Verdadeiro**|O caminho de destino é armazenado em uma variável. Ao selecionar esse valor, a opção dinâmica **RemoteVariable**será exibida.|  
|**Falso**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **RemotePath**será exibida.|  
  
 **OverwriteFileAtDestination**  
 Especifique se um arquivo no destino pode ser substituído.  
  
 **IsLocalPathVariable**  
 Indique se o caminho local deve ser armazenado em uma variável. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Verdadeiro**|O caminho de destino é armazenado em uma variável. Ao selecionar esse valor, a opção dinâmica **LocalVariable**será exibida.|  
|**Falso**|O caminho de destino é especificado em um gerenciador de conexões de Arquivo. Ao selecionar esse valor, a opção dinâmica **LocalPath**será exibida.|  
  
 **Operação**  
 Selecione a operação FTP a executar. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Enviar arquivos**|Enviar arquivos. Ao selecionar esse valor, as opções dinâmicas **LocalVariable**, **LocalPathRemoteVariable** e **RemotePath**serão exibidas.|  
|**Receber arquivos**|Receber arquivos. Ao selecionar esse valor, as opções dinâmicas **LocalVariable**, **LocalPathRemoteVariable** e **RemotePath**serão exibidas.|  
|**Criar diretório local**|Criar um diretório local. Ao selecionar esse valor, as opções dinâmicas **LocalVariable** e **LocalPath**serão exibidas.|  
|**Criar diretório remoto**|Criar um diretório remoto. Ao selecionar esse valor, as opções dinâmicas **RemoteVariable** e **RemotelPath**serão exibidas.|  
|**Remover diretório local**|Remover diretório local. Ao selecionar esse valor, as opções dinâmicas **LocalVariable** e **LocalPath**serão exibidas.|  
|**Remover diretório remoto**|Remover um diretório remoto. Ao selecionar esse valor, as opções dinâmicas **RemoteVariable** e **RemotePath**serão exibidas.|  
|**Excluir arquivos locais**|Excluir arquivos locais. Ao selecionar esse valor, as opções dinâmicas **LocalVariable** e **LocalPath**serão exibidas.|  
|**Excluir arquivos remotos**|Excluir arquivos remotos. Ao selecionar esse valor, as opções dinâmicas **RemoteVariable** e **RemotePath**serão exibidas.|  
  
 **IsTransferASCII**  
 Indique se os arquivos transferidos para e do servidor FTP remoto devem ser transferidos em modo ASCII.  
  
## <a name="isremotepathvariable-dynamic-options"></a>Opções dinâmicas de IsRemotePathVariable  
  
### <a name="isremotepathvariable--true"></a>IsRemotePathVariable = True  
 **RemoteVariable**  
 Selecione uma variável definida pelo usuário existente ou clique em \<**Nova variável...** > para criar uma variável definida pelo usuário.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), Adicionar variável  
  
### <a name="isremotepathvariable--false"></a>IsRemotePathVariable = False  
 **RemotePath**  
 Selecione um gerenciador de conexões FTP existente ou clique em \<**Nova conexão…** > para criar um gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de Conexões de FTP](connection-manager/ftp-connection-manager.md), [Editor do Gerenciador de Conexões de FTP](../../2014/integration-services/ftp-connection-manager-editor.md)  
  
## <a name="islocalpathvariable-dynamic-options"></a>Opções dinâmicas de IsLocalPathVariable  
  
### <a name="islocalpathvariable--true"></a>IsLocalPathVariable = True  
 **LocalVariable**  
 Selecione uma variável definida pelo usuário existente ou clique em \<**Nova variável...** > para criar uma variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), Adicionar variável  
  
### <a name="islocalpathvariable--false"></a>IsLocalPathVariable = False  
 **LocalPath**  
 Selecione um gerenciador de conexões de arquivos existente ou clique em \<**Nova conexão…** > para criar um gerenciador de conexões.  
  
 **Tópicos relacionados**: [Gerenciador de Conexão de arquivo simples](connection-manager/file-connection-manager.md), [Editor do Gerenciador de Conexão de arquivos](../../2014/integration-services/file-connection-manager-editor.md)  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da Tarefa FTP &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Página Expressões](expressions/expressions-page.md)  
  
  
