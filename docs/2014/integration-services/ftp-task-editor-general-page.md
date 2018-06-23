---
title: Editor da tarefa FTP (página geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.ftptask.general.f1
helpviewer_keywords:
- File Transfer Protocol Task Editor
ms.assetid: 28b46fdd-b04a-4f97-a99f-883f5735a6d9
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 786f0d4371773f77045f0ef9cd6825057c12a937
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117220"
---
# <a name="ftp-task-editor-general-page"></a>Editor da Tarefa FTP (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor da Tarefa FTP** para especificar o gerenciador de conexões que estabelece conexão com o servidor FTP com o qual a tarefa se comunica. Você também pode nomear e descrever a tarefa FTP.  
  
 Para obter informações sobre essa tarefa, consulte [Tarefa FTP](control-flow/ftp-task.md).  
  
## <a name="options"></a>Opções  
 **FtpConnection**  
 Selecione um gerenciador de conexões FTP existente ou clique em \<**Nova conexão…**> para criar um gerenciador de conexões.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa FTP &#40;página de transferência de arquivos&#41;](../../2014/integration-services/ftp-task-editor-file-transfer-page.md)   
 [Página Expressões](expressions/expressions-page.md)  
  
  