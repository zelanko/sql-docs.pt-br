---
title: Exemplos de Tarefa Script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], examples
- examples [Integration Services]
- SSIS Script task, examples
ms.assetid: b0dd77ee-ee11-4cd9-87aa-61dd67f2fe1c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 858ca145f28e8f0ea4dd5543b4f6ff6eb6b3e9f6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793684"
---
# <a name="script-task-examples"></a>Exemplos de tarefa Script
  A tarefa Script é uma ferramenta com vários fins que pode ser usada em um pacote para preencher quase todos os requisitos que não sejam satisfeitos pelas tarefas incluídas no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Este tópico lista exemplos de código da tarefa Script, que demonstram algumas das funcionalidades disponíveis.  
  
> [!NOTE]  
>  Se desejar criar tarefas mais fáceis de serem reutilizadas em vários pacotes, procure utilizar o código desses exemplos de tarefa Script como o ponto inicial para tarefas personalizadas. Para obter mais informações, consulte [Desenvolvendo uma tarefa personalizada](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
### <a name="example-topics"></a>Tópicos de exemplo  
 Esta seção contém exemplos de código que demonstram vários usos das classes [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que você pode incorporar em uma tarefa Script do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:  
  
 [Detectar um arquivo simples vazio com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/detecting-an-empty-flat-file-with-the-script-task.md)  
 Verifica um arquivo simples para determinar se ele contém linhas de dados e salva o resultado em uma variável para ser usado na ramificação do fluxo de controle.  
  
 [Obter uma lista para o loop ForEach com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/gathering-a-list-for-the-foreach-loop-with-the-script-task.md)  
 Coleta uma lista de arquivos que satisfazem critérios especificados pelo usuário e preenche uma variável para ser usada posteriormente pelo Enumerador Foreach de Variável.  
  
 [Consultar o Active Directory com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/querying-the-active-directory-with-the-script-task.md)  
 Recupera informações de usuário do Active Directory com base no valor de uma variável do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], usando classes no namespace System.DirectoryServices.  
  
 [Monitorar contadores de desempenho com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/monitoring-performance-counters-with-the-script-task.md)  
 Cria um contador de desempenho personalizado que pode ser usado para rastrear o progresso da execução de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], usando classes no namespace System.Diagnostics.  
  
 [Trabalhar com imagens com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/working-with-images-with-the-script-task.md)  
 Compacta imagens no formato JPEG e cria imagens de miniatura, usando classes no namespace System.Drawing.  
  
 [Localizar impressoras instaladas com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/finding-installed-printers-with-the-script-task.md)  
 Localiza impressoras instaladas compatíveis com um tamanho de papel específico, usando classes no namespace System.Drawing.Printing.  
  
 [Enviar uma mensagem de email HTML com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/sending-an-html-mail-message-with-the-script-task.md)  
 Envia uma mensagem de email em formato HTML em vez de formato de texto sem-formatação.  
  
 [Trabalhar com arquivos do Excel com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
 Lista as planilhas em um arquivo de Excel e verifica a existência de uma planilha específica.  
  
 [Enviar a uma fila de mensagens particular remota com a tarefa Script](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)  
 Envia uma mensagem para uma fila de mensagens privada remota.  
  
### <a name="other-examples"></a>Outros exemplos  
 Os tópicos a seguir também contêm exemplos de código para uso com a tarefa Script:  
  
 [Usar variáveis na tarefa Script](../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)  
 Solicita que o usuário confirme se o pacote deve continuar sendo executado, com base no valor de uma variável de pacote que pode exceder o limite especificado em outra variável.  
  
 [Conectar-se a fontes de dados na tarefa Script](../../integration-services/extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md)  
 Recupera uma conexão ou informações de conexão de gerenciadores de conexões definidos no pacote.  
  
 [Gerar eventos na tarefa Script](../../integration-services/extending-packages-scripting/task/raising-events-in-the-script-task.md)  
 Aumenta um erro, uma advertência ou uma mensagem informativa com base no status da conexão de Internet no servidor.  
  
 [Registrar a tarefa Script em log](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)  
 Registra o número de itens processados pela tarefa para provedores de log habilitados.  
  
  
