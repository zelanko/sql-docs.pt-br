---
title: Arquivos de banco de dados de origem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.sourcedbfiles.f1
ms.assetid: 7dc6bfeb-37c1-45e8-a705-a87564922265
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ac7d4b590fa5c3efccd16deebf3bafab83b74f6b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055542"
---
# <a name="source-database-files"></a>Arquivos de banco de dados de origem
  Use a caixa de diálogo **Arquivos de Banco de Dados de Origem** para visualizar os nomes e locais do arquivo do banco de dados no servidor de origem ou especificar um local de compartilhamento de arquivos na rede para a tarefa Transferir Banco de Dados. Para obter mais informações sobre essa tarefa, consulte [Tarefa Transferir Banco de Dados](control-flow/transfer-database-task.md).  
  
 Para popular esta caixa de diálogo com os nomes e locais dos arquivos do banco de dados no servidor de origem, especifique primeiro **SourceConnection** e **SourceDatabaseName** na página **Banco de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
## <a name="options"></a>Opções  
 **Arquivo de origem**  
 Nomes do arquivo de banco de dados no servidor de origem que serão transferidos. O **arquivo de origem** é somente leitura.  
  
 **Pasta de origem**  
 Pasta no servidor de origem em que residem os arquivos de banco de dados a serem transferidos. A **pasta de origem** é somente leitura.  
  
 **Compartilhamento de arquivos de rede**  
 Pasta de compartilhamento de rede no servidor de origem da qual os arquivos de banco de dados serão transferidos. Use **o compartilhamento de arquivos de rede** ao transferir um banco de dados no modo offline especificando **DatabaseOffline em** para o **método** na página **bancos** de dados da caixa de diálogo **Editor da tarefa Transferir Banco de dados** .  
  
 Insira a localização de compartilhamento de arquivos na rede ou clique no botão Procurar **(...)** para localizá-la.  
  
 Na transferência de um banco de dados em modo offline, os arquivos de banco de dados são copiados para o local **Compartilhamento de arquivo na rede** no servidor de origem, antes de serem transferidos ao servidor de destino.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa Transferir Banco de dados &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor da tarefa Transferir Banco de dados &#40;página bancos de dados&#41;](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
