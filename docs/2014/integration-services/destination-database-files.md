---
title: Arquivos de banco de dados de destino | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.destdbfiles.f1
ms.assetid: f6f90417-86fb-4b8c-a790-0b215c344ef6
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fb6f834ab26fb6d5cc7535d217745af92e97c2a5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135266"
---
# <a name="destination-database-files"></a>Arquivos de banco de dados de destino
  Use a caixa de diálogo **Arquivos do Banco de Dados de Destino** para exibir ou alterar os nomes e locais dos arquivos de banco de dados no servidor de destino ou especificar um local de arquivos na rede para a tarefa Transferir Banco de Dados. Para obter mais informações sobre essa tarefa, consulte [Tarefa Transferir Banco de Dados](control-flow/transfer-database-task.md).  
  
 Para popular automaticamente essa caixa de diálogo com os locais e nomes de arquivos no servidor de origem, especifique o **SourceConnection**, **SourceDatabaseName**, e **SourceDatabaseFiles** primeiro na página **Bancos de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
## <a name="options"></a>Opções  
 **Arquivo de Destino**  
 Nomes dos arquivos de banco de dados transferidos no servidor de destino.  
  
 Digite o nome do arquivo ou clique no nome do arquivo para editá-lo.  
  
 **Pasta de Destino**  
 Pasta no servidor de destino para onde os arquivos de banco de dados serão transferidos.  
  
 Digite o caminho da pasta, clique no caminho da pasta para editá-lo ou clique em procurar para localizar a pasta onde você quer transferir os arquivos de banco de dados no servidor de destino.  
  
 **Compartilhamento de Arquivos na Rede**  
 Pasta compartilhada de rede no servidor de destino para o qual os arquivos de banco de dados serão transferidos. Use **Compartilhamento de arquivo na rede** ao transferir um banco de dados em modo offline, especificando **DatabaseOffline** em **Método** na página **Banco de Dados** da caixa de diálogo **Editor da Tarefa Transferir Banco de Dados** .  
  
 Insira o local de compartilhamento de arquivos na rede ou clique em Procurar para localizá-lo.  
  
 Ao transferir um banco de dados em modo offline, os arquivos de banco de dados são copiados para o local **Compartilhamento de arquivo na rede** antes de serem transferidos para o local **Pasta de destino** .  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor da tarefa de banco de dados transferir &#40;página geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor da tarefa de banco de dados transferir &#40;página de bancos de dados&#41;](../../2014/integration-services/transfer-database-task-editor-databases-page.md)  
  
  
