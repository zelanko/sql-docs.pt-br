---
title: 'Tarefa 9: Configurando um serviço de dados de referência | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e4c756463c43ede8c6dae0cda0a184f0ec7f9956
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "70154928"
---
# <a name="task-9-configuring-a-reference-data-service"></a>Tarefa 9: Configurando um serviço de dados de referência
  Nesta tarefa, você configura o DQS para usar um serviço de dados de referência no Azure Marketplace. Na próxima tarefa, você configurará o domínio de **validação de endereço** para usar esse serviço. No tempo de execução, durante a atividade de limpeza, o DQS passa os valores dos domínios no domínio de **validação de endereço** para o serviço para limpeza. Consulte [Configurar o DQS para usar dados de referência](https://msdn.microsoft.com/library/hh213070.aspx) para obter mais detalhes.  
  
1.  Na página principal do **cliente do DQS**, no painel **Administração** , clique em **configuração**.  
  
2.  Verifique se a guia **dados de referência** está ativa.  
  
3.  Na área **configurações de rede** , digite os valores apropriados nos campos **servidor proxy** e **porta** se você precisar usar um servidor proxy para se conectar à Internet.  
  
4.  Digite sua **chave de conta do Azure Marketplace** para o campo **ID da conta do DataMarket** .  
  
     ![Conta do Serviço de Dados de Referência do Azure Data Market](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Conta do Serviço de Dados de Referência do Azure Data Market")  
  
5.  Clique no botão **validar** ao lado da caixa de texto para validar a ID da conta.  
  
6.  Clique em **OK** na caixa de mensagem.  
  
7.  Clique em **fechar** na parte inferior da página para alternar para a página principal do cliente do DQS.  
  
## <a name="next-task"></a>Próxima tarefa  
 [Tarefa 10: Configurando o domínio composto para usar o serviço de dados de referência](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
