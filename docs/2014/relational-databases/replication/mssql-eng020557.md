---
title: MSSQL_ENG020557 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020557 error
ms.assetid: c43c6952-5b60-4347-b881-11a0004dce24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6816a0301a03e2c0d01cfe78a5c88213394c445b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63057099"
---
# <a name="mssql_eng020557"></a>MSSQL_ENG020557
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|20557|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|Desligamento do agente. Para obter mais informações, consulte o histórico de trabalho do SQL Server Agent relacionado ao trabalho '%s'.|  
  
## <a name="explanation"></a>Explicação  
 Um agente de replicação foi desligado sem gravar um motivo para a tabela de histórico apropriada ou, então, o agente foi desligado no meio de um processo.  
  
## <a name="user-action"></a>Ação do usuário  
  
-   Reinicie o agente para verificar se agora será possível executá-lo sem falhas. Para obter mais informações, consulte [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) e [Conceitos dos executáveis do agente de replicação](concepts/replication-agent-executables-concepts.md).  
  
-   Verifique o histórico de agente e o histórico de trabalho para outros erros que aconteceram quase no mesmo momento. Para obter informações sobre como exibir detalhes de status e de erro do agente no Replication Monitor, confira [Exibir informações e executar tarefas usando o Replication Monitor](monitor/view-information-and-perform-tasks-replication-monitor.md).
-   Verifique se a conectividade básica está funcionado entre os computadores acessados pelo agente e, em seguida, conecte-se a cada computador usando um utilitário, como o **sqlcmd** . Ao se conectar, use a mesma conta com a qual o agente faz conexões. Para obter mais informações sobre as permissões necessárias para cada conta de agente, consulte [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
-   Se o erro ocorrer ao criar ou aplicar um instantâneo, verifique os arquivos no diretório de instantâneos com relação a erros.  
  
-   Se o erro continuar ocorrendo, aumente o log do agente e especifique um arquivo de saída para o log. Dependendo do contexto do erro, isso poderá fornecer as etapas que levam ao erro e às mensagens de erro adicionais. Para obter mais informações sobre como configurar o log para replicação, consulte o artigo [312292](https://support.microsoft.com/kb/312292)na Base de Dados de Conhecimento Microsoft.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
