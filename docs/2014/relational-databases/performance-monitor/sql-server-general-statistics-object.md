---
title: SQL Server, objeto Estatísticas Gerais | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:General Statistics
- General Statistics object
ms.assetid: c738e549-d7e7-4211-9ec3-064ac140af7c
caps.latest.revision: 24
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 48b8df37c64ea017445f1e44cd6e03603708fa86
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43820752"
---
# <a name="sql-server-general-statistics-object"></a>SQL Server, objeto General Statistics
  O objeto **SQLServer:General Statistics** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar a atividade geral em todo o servidor, como o número de conexões atuais e o número de usuários que se conectam e se desconectam, por segundo, dos computadores que executam uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso pode ser útil ao trabalhar com sistemas do tipo OLTP, em que há muitos clientes conectando-se e desconectando-se de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Esta tabela descreve os contadores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **do** .  
  
|Contadores de Estatísticas Gerais do SQL Server|Description|  
|--------------------------------------------|-----------------|  
|**Tabelas Temporárias Ativas**|Número de tabelas temporárias/variáveis de tabela em uso.|  
|**Redefinições de conexão/s**|O número total de logons iniciados do pool de conexão.|  
|**Cancelamento Atrasado das Notificações de Eventos**|Número de notificações de eventos aguardando serem descartadas por um thread do sistema.|  
|**Solicitações HTTP Autenticadas**|Número de solicitações HTTP autenticadas iniciadas por segundo.|  
|**Conexões Lógicas**|Número de conexões lógicas com o sistema.<br /><br /> A finalidade principal de conexões lógicas é atender às solicitações de MARS (vários conjuntos de resultados ativos). Para as solicitações de MARS, sempre que um aplicativo estabelecer uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], poderá haver mais de uma conexão lógica que corresponda a uma conexão física.<br /><br /> Quando o MARS não é usado, a proporção entre conexões físicas e lógicas é de 1:1. Portanto, sempre que um aplicativo estabelece uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as conexões lógicas aumentam em 1.|  
|**Logons/s**|Número total de logons iniciados por segundo. Isso não inclui conexões em pool.|  
|**Logoffs/s**|Número total de operações de logoff iniciadas por segundo.|  
|**Deadlocks MARS**|Número de deadlocks MARS detectados.|  
|**Taxa de concessão não atômica**|Número de concessões não atômicas por segundo.|  
|**Processos bloqueados**|Número de processos bloqueados atualmente.|  
|**Solicitações SOAP Vazias**|Número de solicitações SOAP vazias iniciadas por segundo.|  
|**Invocações do Método SOAP**|Número de invocações do método SOAP iniciadas por segundo.|  
|**Solicitações de Início da Sessão SOAP**|Número de solicitações de início da sessão SOAP iniciadas por segundo.|  
|**Solicitações de Término da Sessão SOAP**|Número de solicitações de término da sessão SOAP iniciadas por segundo.|  
|**Solicitações SOAP SQL**|Número de solicitações SOAP SQL iniciadas por segundo.|  
|**Solicitações SOAP WSDL**|Número de solicitações SOAP WSDL (Web Service Description Language) iniciadas por segundo.|  
|**Taxa de Criação de Tabelas Temporárias**|Número de tabelas temporárias/variáveis de tabelas criadas por segundo.|  
|**Tabelas Temporárias para Destruição**|Número de tabela temporárias/variáveis de tabela que aguardam serem destruídas pelo thread de limpeza do sistema.|  
|**Fila de Notificações de Eventos de Rastreamento**|Número de instâncias de notificações de eventos de rastreamento que aguardam na fila interna para serem enviadas pelo Service Broker.|  
|**Transações**|Número de inscrições de transações (combinações de locais, DTC e acopladas).|  
|**Conexões de Usuário**|Conta o número de usuários atualmente conectados ao SQL Server.|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
