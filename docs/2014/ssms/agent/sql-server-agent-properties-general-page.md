---
title: Propriedades do SQL Server Agent (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 66a7b7cd9328f70e5b5ca374a04ad5e9dd6e079a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245776"
---
# <a name="sql-server-agent-properties-general-page"></a>Propriedades do SQL Server Agent (página Geral)
  Use esta página para exibir e modificar as propriedades gerais do serviço [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Agent.  
  
## <a name="options"></a>Opções  
 **Estado do serviço**  
 Exibe o estado atual do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Reinicialização automática SQL Server se parar inesperadamente**  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent reiniciará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parar inesperadamente.  
  
 **Reinicialização automática SQL Server Agent se parar inesperadamente**  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reiniciará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent parar inesperadamente.  
  
 **Nome do arquivo**  
 Especifica o nome do arquivo para o log de erros.  
  
 **...**  
 Navegue até o arquivo de log de erros.  
  
 **Incluir mensagens de rastreamento de execução**  
 Inclui mensagens de rastreamento de execução no log de erros. As mensagens de rastreamento fornecem informações detalhadas sobre a operação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Portanto, o arquivo de log requer mais espaço em disco quando essa opção é selecionada. Essa opção só deve ser selecionada ao solucionar um problema que possa envolver o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Gravar arquivo OEM**  
 Grava o arquivo de log de erros como um arquivo não Unicode. Isso reduz a quantidade de espaço em disco consumida pelo arquivo de log. Porém, mensagens que incluem dados Unicode podem ser mais difíceis de ler quando essa opção é habilitada.  
  
 **Destinatário do net send**  
 Digite o nome de um operador para receber a notificação net send das mensagens que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent gravar no arquivo de log.  
  
## <a name="see-also"></a>Consulte Também  
 [Operações](operators.md)   
 [Log de erros do SQL Server Agent](sql-server-agent-error-log.md)  
  
  
