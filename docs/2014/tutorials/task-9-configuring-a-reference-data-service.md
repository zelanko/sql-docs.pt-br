---
title: 'Tarefa 9: Configurando um serviço de dados de referência | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5a08d3848ddaf65b9e10b654f55e8a0a4d9be690
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131035"
---
# <a name="task-9-configuring-a-reference-data-service"></a>Tarefa 9: Configurando um serviço de dados de referência
  Nesta tarefa, você configurará o DQS para usar um Serviço de Dados de Referência no Windows Azure Marketplace. A próxima tarefa, você configurará o **Address Validation** domínio para usar este serviço. Em tempo de execução, durante a atividade de limpeza DQS passa os valores de domínios a **Address Validation** domínio para o serviço de limpeza. Consulte [configurar DQS para usar dados de referência](http://msdn.microsoft.com/library/hh213070.aspx) para obter mais detalhes.  
  
1.  Na página principal do **cliente DQS**, além de **administração** painel, clique em **configuração**.  
  
2.  Certifique-se de que **dados de referência** guia está ativa.  
  
3.  No **as configurações de rede** área, digite os valores apropriados no **servidor Proxy** e **porta** campos se você precisar usar um servidor proxy para se conectar à Internet.  
  
4.  Tipo de sua **chave de conta do Windows Azure Marketplace** para o **ID da conta DataMarket** campo.  
  
     ![Conta do serviço de dados do Azure Data Market referência](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "conta do serviço de dados do Azure Data Market referência")  
  
5.  Clique em **validar** botão ao lado da caixa de texto para validar a ID de conta.  
  
6.  Clique em **OK** na caixa de mensagem.  
  
7.  Clique em **fechar** na parte inferior da página para alternar para a página principal do cliente do DQS.  
  
## <a name="next-task"></a>Próxima tarefa  
 [Tarefa 10: Configurando o domínio composto para usar o serviço de dados de referência](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  