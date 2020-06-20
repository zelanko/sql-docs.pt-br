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
ms.openlocfilehash: bb40764ee279d98b6b63906ed08b26afe156aee4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962856"
---
# <a name="source-database-files"></a>Arquivos de banco de dados de origem
  Use a caixa de diálogo **Arquivos de Banco de Dados de Origem** para visualizar os nomes e locais do arquivo do banco de dados no servidor de origem ou especificar um local de compartilhamento de arquivos na rede para a tarefa Transferir Banco de Dados. Para obter mais informações sobre essa tarefa, consulte [Tarefa Transferir Banco de Dados](control-flow/transfer-database-task.md).  
  
 Para popular esta caixa de diálogo com os nomes e locais dos arquivos do banco de dados no servidor de origem, especifique primeiro **SourceConnection** e **SourceDatabaseName** na página **Banco de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
## <a name="options"></a>Opções  
 **Arquivo de origem**  
 Nomes do arquivo de banco de dados no servidor de origem que serão transferidos. O**Arquivo de Origem** é somente leitura.  
  
 **Pasta de Origem**  
 Pasta no servidor de origem em que residem os arquivos de banco de dados a serem transferidos. A**Pasta de Origem** é somente leitura.  
  
 **Compartilhamento de Arquivos na Rede**  
 Pasta de compartilhamento de rede no servidor de origem da qual os arquivos de banco de dados serão transferidos. Use **Compartilhamento de Arquivo na Rede** ao transferir um banco de dados em modo offline, especificando **DatabaseOffline** em **Método** na página **Banco de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
 Insira o local do compartilhamento de arquivos de rede ou clique no botão procurar **(...)** para localizar o local de compartilhamento de arquivos de rede.  
  
 Na transferência de um banco de dados em modo offline, os arquivos de banco de dados são copiados para o local **Compartilhamento de arquivo na rede** no servidor de origem, antes de serem transferidos ao servidor de destino.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa Transferir Banco de dados &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor da Tarefa Transferir Banco de Dados &#40;Página Bancos de Dados&#41;](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
