---
title: "Propriedades do SQL Server Agent (página Geral) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4046c9c45fda98646043e73c8a9b1e1bacfdd335
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-agent-properties-general-page"></a>Propriedades do SQL Server Agent (página Geral)
Use esta página para exibir e modificar as propriedades gerais do serviço do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Estado do serviço**  
Exibe o estado atual do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
**Reiniciar automaticamente o SQL Server se ele parar inesperadamente**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] O Agent reiniciará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] parar inesperadamente.  
  
**Reiniciar automaticamente o SQL Server Agent se ele parar inesperadamente**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] reiniciará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent parar inesperadamente.  
  
**Filename**  
Especifica o nome do arquivo para o log de erros.  
  
**...**  
Navegue até o arquivo de log de erros.  
  
**Incluir mensagens de rastreamento de execução**  
Inclui mensagens de rastreamento de execução no log de erros. As mensagens de rastreamento fornecem informações detalhadas sobre a operação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Portanto, o arquivo de log requer mais espaço em disco quando essa opção é selecionada. Essa opção só deve ser selecionada ao solucionar um problema que possa envolver o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
**Gravar arquivo OEM**  
Grava o arquivo de log de erros como um arquivo não Unicode. Isso reduz a quantidade de espaço em disco consumida pelo arquivo de log. Porém, mensagens que incluem dados Unicode podem ser mais difíceis de ler quando essa opção é habilitada.  
  
**Destinatário do net send**  
Digite o nome de um operador para receber a notificação net send das mensagens que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent gravar no arquivo de log.  
  
## <a name="see-also"></a>Consulte também  
[Operadores](../../ssms/agent/operators.md)  
[Log de erros do SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
