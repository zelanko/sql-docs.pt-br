---
title: "Propriedades do servidor (p&#225;gina Diversas Configura&#231;&#245;es de Servidor) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.serverproperties.miscserversettings.f1"
ms.assetid: b170c066-30cd-42dd-8d34-aa129ea09551
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 22
---
# Propriedades do servidor (p&#225;gina Diversas Configura&#231;&#245;es de Servidor)
  Use esta página para exibir ou modificar as configurações de servidor.  
  
## Opções  
 **Linguagem padrão para usuários**  
 Especifica a linguagem padrão para todos os logons recém-criados.  
  
 **Permitir que gatilhos acionem outros gatilhos**  
 Controla se um gatilho pode executar uma ação que inicia outro gatilho. Quando desmarcado, os gatilhos não podem ser acionados por outro gatilho. Quando selecionado, os gatilhos podem ser acionados por outros gatilhos em até 32 níveis.  
  
 **Usar administrador de consultas para evitar consultas demoradas**  
 Especifica um limite superior de tempo em que uma consulta pode ser executada. O custo da consulta refere-se ao tempo decorrido estimado, em segundos, necessário para executar uma consulta em uma configuração de hardware específica. Por padrão, o administrador de consultas é desativado e todas as consultas têm permissão para serem executadas. Se essa opção for selecionada, você deve digitar um limite de tempo na caixa de texto abaixo. Se você especificar um valor que não seja zero nem negativo, o administrador de consultas recusará a execução de qualquer consulta com um custo estimado que exceda aquele valor.  
  
 **Interpretar um ano de dois dígitos como incluído entre**  
 Especifica o intervalo de datas de 100 anos para interpretar valores de anos com dois dígitos. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpretará valores de datas de dois dígitos como referências ao final do ano com esses dígitos e que se inclui no intervalo especificado.  
  
 Define a caixa à direita com o ano final. Quando o ano final for salvo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] populará automaticamente a caixa com o ano inicial.  
  
 **Valores Configurados**  
 Exibe os valores configurados para as opções nesse painel. Se você alterar esses valores, clique em **Executando Valores** para verificar se as alterações entraram em vigor. Se as alterações não entraram em vigor, a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser redeclarada primeiro.  
  
 **Executando Valores**  
 Exiba os valores que estão sendo executados para as opções neste painel. Esses valores são somente leitura.  
  
## Consulte também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  