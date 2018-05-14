---
title: Configurar um servidor para executar a política desativada por padrão | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 41c3022d-ab13-443e-ac64-ba1d64584f79
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: bd8198d4ab869b38491a58782a03e73d2aaecb5c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-2---configure-a-server-to-run-the-off-by-default-policy"></a>Lição 1-2 – Configurar um servidor para executar a política desativada por padrão
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Agora você tem uma política chamada Desativada por Padrão. Nesta tarefa, você verificará se o servidor está em conformidade com os requisitos dessa política.  
  
### <a name="to-run-the-off-by-default-policy"></a>Para executar a política Desativada por Padrão  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aponte para **Políticas**e clique em **Avaliar**.  
  
2.  Na caixa de diálogo **Avaliar Políticas** , você pode selecionar as políticas de outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de um arquivo. Nesta etapa, deixe **Fonte** definida para a sua instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
3.  Na seção **Políticas** , selecione a política **Desativada por Padrão** .  
  
4.  Para ver se o servidor está em conformidade com a política, clique em **Avaliar**.  
  
5.  Na área **Resultados** , você verá um círculo verde com uma marca de seleção se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] estiver em conformidade com a política. Você verá um círculo vermelho com um X se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não obedecer a política.  
  
6.  Na área **Detalhes de Destino** , você verá informações adicionais na coluna **Mensagem** se ocorrer algum erro. Na coluna **Mensagem** , clique em **Exibir** para ver um relatório com os resultados da verificação de cada propriedade de faceta verificada.  
  
7.  A descrição da política é exibida na parte inferior da página, e a seção **Ajuda adicional** exibe o hiperlink configurado para a política. Clique no hiperlink da mensagem para abrir a página da Web que você especificou quando criou a política.  
  
8.  Feche o navegador e a caixa de diálogo **Exibição Detalhada dos Resultados** .  
  
9. Se o servidor não estiver em conformidade e você quiser desabilitar o Database Mail, clique em **Aplicar** na página **Resultados da Avaliação** .  
  
10. Feche as caixas de diálogo **Exibição Detalhada dos Resultados** e **Avaliar Políticas** .  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 2: Criar e aplicar uma política de nomeação de padrões](../../relational-databases/policy-based-management/lesson-2-create-and-apply-a-naming-standards-policy.md)  
  
  
  
