---
title: Arquivos de banco de dados de destino | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.destdbfiles.f1
ms.assetid: f6f90417-86fb-4b8c-a790-0b215c344ef6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2cfee31b4167625b4f868d7312abd752a215652c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66059552"
---
# <a name="destination-database-files"></a>Arquivos de banco de dados de destino
  Use a caixa de diálogo **Arquivos do Banco de Dados de Destino** para exibir ou alterar os nomes e locais dos arquivos de banco de dados no servidor de destino ou especificar um local de arquivos na rede para a tarefa Transferir Banco de Dados. Para obter mais informações sobre essa tarefa, consulte [Tarefa Transferir Banco de Dados](control-flow/transfer-database-task.md).  
  
 Para popular automaticamente essa caixa de diálogo com os locais e nomes de arquivos no servidor de origem, especifique o **SourceConnection**, **SourceDatabaseName**, e **SourceDatabaseFiles** primeiro na página **Bancos de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
## <a name="options"></a>Opções  
 **Arquivo de destino**  
 Nomes dos arquivos de banco de dados transferidos no servidor de destino.  
  
 Digite o nome do arquivo ou clique no nome do arquivo para editá-lo.  
  
 **Pasta de destino**  
 Pasta no servidor de destino para onde os arquivos de banco de dados serão transferidos.  
  
 Digite o caminho da pasta, clique no caminho da pasta para editá-lo ou clique em procurar para localizar a pasta onde você quer transferir os arquivos de banco de dados no servidor de destino.  
  
 **Compartilhamento de arquivos de rede**  
 Pasta compartilhada de rede no servidor de destino para o qual os arquivos de banco de dados serão transferidos. Use **Compartilhamento de arquivo na rede** ao transferir um banco de dados em modo offline, especificando **DatabaseOffline** em **Método** na página **Banco de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
 Insira o local de compartilhamento de arquivos na rede ou clique em Procurar para localizá-lo.  
  
 Ao transferir um banco de dados em modo offline, os arquivos de banco de dados são copiados para o local **Compartilhamento de arquivo na rede** antes de serem transferidos para o local **Pasta de destino** .  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa Transferir Banco de dados &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor da tarefa Transferir Banco de dados &#40;página bancos de dados&#41;](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
