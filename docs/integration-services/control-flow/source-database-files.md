---
title: Arquivos de banco de dados de origem | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1
ms.assetid: 7dc6bfeb-37c1-45e8-a705-a87564922265
caps.latest.revision: 17
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0fb66420c0073a79ba6b78608de09fd901c738c0
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="source-database-files"></a>Arquivos de banco de dados de origem
  Use a caixa de diálogo **Arquivos de Banco de Dados de Origem** para visualizar os nomes e locais do arquivo do banco de dados no servidor de origem ou especificar um local de compartilhamento de arquivos na rede para a tarefa Transferir Banco de Dados. Para obter mais informações sobre essa tarefa, consulte [Tarefa Transferir Banco de Dados](../../integration-services/control-flow/transfer-database-task.md).  
  
 Para popular esta caixa de diálogo com os nomes e locais dos arquivos do banco de dados no servidor de origem, especifique primeiro **SourceConnection** e **SourceDatabaseName** na página **Banco de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
## <a name="options"></a>Opções  
 **Arquivo de Origem**  
 Nomes do arquivo de banco de dados no servidor de origem que serão transferidos. O**Arquivo de Origem** é somente leitura.  
  
 **Pasta de Origem**  
 Pasta no servidor de origem em que residem os arquivos de banco de dados a serem transferidos. A**Pasta de Origem** é somente leitura.  
  
 **Compartilhamento de Arquivos na Rede**  
 Pasta de compartilhamento de rede no servidor de origem da qual os arquivos de banco de dados serão transferidos. Use **Compartilhamento de Arquivo na Rede** ao transferir um banco de dados em modo offline, especificando **DatabaseOffline** em **Método** na página **Banco de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
 Insira o local de compartilhamento de arquivos na rede ou clique no botão Procurar **(...)** para localizá-lo.  
  
 Na transferência de um banco de dados em modo offline, os arquivos de banco de dados são copiados para o local **Compartilhamento de arquivo na rede** no servidor de origem, antes de serem transferidos ao servidor de destino.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa transferir banco de dados &#40; Página geral &#41;](../../integration-services/control-flow/transfer-database-task-editor-general-page.md)   
 [Editor da tarefa transferir banco de dados &#40; página bancos de dados &#41;](../../integration-services/control-flow/transfer-database-task-editor-databases-page.md)  
  
  
