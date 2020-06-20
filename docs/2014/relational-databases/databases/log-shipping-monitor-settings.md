---
title: Configurações do Monitor de Envio de Logs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.logshipping.settings.monitor.f1
ms.assetid: 45e2ba7d-b3aa-4643-9451-bcb991572314
author: stevestein
ms.author: sstein
ms.openlocfilehash: dcf8810d43f69acc858a0882ad17aa1056014ca7
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965926"
---
# <a name="log-shipping-monitor-settings"></a>Configurações do monitor de envio de logs
  Use essa página para configurar e modificar as propriedades do servidor monitor para envio de logs.  
  
 Para obter uma explicação dos conceitos de envio de log, veja [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opções  
 **Instância de Servidor Monitor**  
 Exibe o nome da instância do servidor configurada presentemente como servidor monitor para a configuração do envio de logs.  
  
 **Connect**  
 Escolha e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usada como servidor monitor. A conta usada para conexão precisa ser membro da função de servidor fixa sysadmin na instância de servidor secundário.  
  
 **Representando a conta proxy do trabalho**  
 Faça com que o envio de logs represente a conta do proxy do SQL Server Agent quando conectar-se à instância do servidor monitor. Os processos de backup, cópia e restauração precisam estar preparados para conexão com o servidor monitor para atualizar o status das operações de envio de logs.  
  
 **Usando o seguinte logon do SQL Server**  
 Permita que o envio de logs use um logon [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] específico na conexão com a instância do servidor monitor. Os processos de backup, cópia e restauração precisam estar preparados para conexão com o servidor monitor para atualizar o status das operações de envio de logs. Selecione essa opção para que o envio de logs use um logon específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Em seguida, especifique logon e senha.  
  
 **Excluir histórico após**  
 Especifique o número de horas em que as informações do histórico do log de envio no servidor monitor serão retidas antes de serem excluídas.  
  
 **Nome do trabalho**  
 Indica o nome do trabalho de alerta do SQL Server Agent usado pelo envio de logs para gerar alertas quando os limites de backup e restauração forem excedidos. Ao criar esse trabalho pela primeira vez, é possível alterar o nome digitando-o na caixa.  
  
 **Agenda**  
 Indica a agenda atual do trabalho de alerta do SQL Server Agent.  
  
 **Editar**  
 Modifique os parâmetros do trabalho de alerta do SQL Server Agent.  
  
 **Desabilitar este trabalho**  
 Suspender o trabalho de alerta do SQL Server Agent.  
  
  
