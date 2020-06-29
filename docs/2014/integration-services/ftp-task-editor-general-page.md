---
title: Editor da tarefa FTP (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.ftptask.general.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 28b46fdd-b04a-4f97-a99f-883f5735a6d9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 381493758306e3f7c638f46f7c331f0e6cc3e83f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425313"
---
# <a name="ftp-task-editor-general-page"></a>Editor da Tarefa FTP (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa FTP** para especificar o gerenciador de conexões que estabelece conexão com o servidor FTP com o qual a tarefa se comunica. Você também pode nomear e descrever a tarefa FTP.  
  
 Para obter informações sobre essa tarefa, consulte [Tarefa FTP](control-flow/ftp-task.md).  
  
## <a name="options"></a>Opções  
 **FtpConnection**  
 Selecione um Gerenciador de conexões de FTP existente ou clique em \<**New connection...**> para criar um Gerenciador de conexões.  
  
> [!IMPORTANT]  
>  O gerenciador de conexões de FTP dá suporte apenas para autenticação anônima e autenticação básica. Ele não suporta a Autenticação do Windows.  
  
 **Tópicos relacionados**: [Gerenciador de Conexões de FTP](connection-manager/ftp-connection-manager.md), [Editor do Gerenciador de Conexões de FTP](../../2014/integration-services/ftp-connection-manager-editor.md)  
  
 **StopOnFailure**  
 Indique se a tarefa FTP deve ser encerrada se a operação FTP falhar.  
  
 **Nome**  
 Forneça um nome exclusivo para a tarefa FTP. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa FTP.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa FTP &#40;página transferência de arquivos&#41;](../../2014/integration-services/ftp-task-editor-file-transfer-page.md)   
 [Página Expressões](expressions/expressions-page.md)  
  
  
