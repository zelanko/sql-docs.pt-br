---
title: 'Tarefa 9: Configurando um serviço de dados de referência | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: adbde32de86da407bdd2655f66d036021e6784f8
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56039407"
---
# <a name="task-9-configuring-a-reference-data-service"></a>Tarefa 9: Configurando um serviço de dados de referência
  Nesta tarefa, você configurará o DQS para usar um Serviço de Dados de Referência no Windows Azure Marketplace. A próxima tarefa, você irá configurar o **Address Validation** domínio para usar este serviço. No tempo de execução durante a atividade de limpeza, o DQS passa os valores dos domínios na **Address Validation** domínio para o serviço de limpeza. Ver [configurar DQS para usar dados de referência](https://msdn.microsoft.com/library/hh213070.aspx) para obter mais detalhes.  
  
1.  Na página principal do **cliente DQS**, no **administração** painel, clique em **configuração**.  
  
2.  Certifique-se de que **dados de referência** guia estiver ativa.  
  
3.  No **as configurações de rede** área, digite os valores apropriados na **servidor Proxy** e **porta** campos se você precisar usar um servidor proxy para se conectar à Internet.  
  
4.  Tipo de sua **chave de conta do Windows Azure Marketplace** para o **ID da conta do DataMarket** campo.  
  
     ![Conta de serviço de dados de referência do Azure Data Market](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "conta de serviço de dados de referência do Azure Data Market")  
  
5.  Clique em **validar** botão ao lado da caixa de texto para validar a ID de conta.  
  
6.  Clique em **OK** na caixa de mensagem.  
  
7.  Clique em **fechar** na parte inferior da página para alternar para a página principal do cliente do DQS.  
  
## <a name="next-task"></a>Próxima tarefa  
 [Tarefa 10: Configurando o domínio composto para usar o serviço de dados de referência](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
