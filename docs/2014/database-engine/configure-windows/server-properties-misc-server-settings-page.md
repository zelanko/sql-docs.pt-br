---
title: Propriedades do servidor – página Configurações Diversas do Servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.miscserversettings.f1
ms.assetid: b170c066-30cd-42dd-8d34-aa129ea09551
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d726e1e79b1a3e24aea074c0821e1f8773b233c5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62809326"
---
# <a name="server-properties-misc-server-settings-page"></a>Propriedades do servidor (página Diversas Configurações de Servidor)
  Use esta página para exibir ou modificar as configurações de servidor.  
  
## <a name="options"></a>Opções  
 **Idioma padrão para usuários**  
 Especifica a linguagem padrão para todos os logons recém-criados.  
  
 **Permitir que os gatilhos disparem outros gatilhos**  
 Controla se um gatilho pode executar uma ação que inicia outro gatilho. Quando desmarcado, os gatilhos não podem ser acionados por outro gatilho. Quando selecionado, os gatilhos podem ser acionados por outros gatilhos em até 32 níveis.  
  
 **Usar o administrador de consultas para evitar consultas de longa execução**  
 Especifica um limite superior de tempo em que uma consulta pode ser executada. O custo da consulta refere-se ao tempo decorrido estimado, em segundos, necessário para executar uma consulta em uma configuração de hardware específica. Por padrão, o administrador de consultas é desativado e todas as consultas têm permissão para serem executadas. Se essa opção for selecionada, você deve digitar um limite de tempo na caixa de texto abaixo. Se você especificar um valor que não seja zero nem negativo, o administrador de consultas recusará a execução de qualquer consulta com um custo estimado que exceda aquele valor.  
  
 **Interpretar um ano de dois dígitos como estando entre**  
 Especifica o intervalo de datas de 100 anos para interpretar valores de anos com dois dígitos. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpretará valores de data de dois dígitos para se referir ao ano que termina nesses dígitos que se enquadram dentro do intervalo especificado.  
  
 Define a caixa à direita com o ano final. Quando o ano final for salvo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] populará automaticamente a caixa com o ano inicial.  
  
 **Valores Configurados**  
 Exibe os valores configurados para as opções nesse painel. Se você alterar esses valores, clique em **Executando Valores** para verificar se as alterações entraram em vigor. Se as alterações não entraram em vigor, a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser redeclarada primeiro.  
  
 **Executando Valores**  
 Exiba os valores que estão sendo executados para as opções neste painel. Esses valores são somente leitura.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
