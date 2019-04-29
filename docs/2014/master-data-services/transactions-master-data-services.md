---
title: Transações (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Master Data Services], about transactions
- transactions [Master Data Services]
ms.assetid: 4cd2fa6f-9c76-4b7a-ae18-d4e5fd2f03f5
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: b309669027da801681c1386abe604fce2f915f3d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62923245"
---
# <a name="transactions-master-data-services"></a>Transações (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], uma transação é registrada sempre que uma ação é tomada em um membro. Transações podem ser exibidas por todos os usuários e revertidas por administradores. As transações mostram a data, a hora e o usuário que tomou a ação, além de outros detalhes. Usuários podem adicionar uma anotação a uma transação, para indicar por que uma transação aconteceu.  
  
## <a name="when-transaction-are-recorded"></a>Quando as transações são registradas  
 As transações são registradas quando os membros:  
  
-   São criados, excluídos ou reativados.  
  
-   Têm valores de atributo alterados.  
  
-   São movidos em uma hierarquia.  
  
 As transações não são gravadas quando as regras de negócios alteram os valores do atributo.  
  
## <a name="view-and-manage-transactions"></a>Exibir e gerenciar transações  
 Na área funcional **Explorer** , você pode exibir e anotar (adicionar comentários) as transações que você mesmo criou.  
  
 Na área funcional **Gerenciamento de Versões** , os administradores podem exibir todas as transações de todos os usuários dos modelos aos quais têm acesso e reverter qualquer uma dessas transações.  
  
> [!NOTE]  
>  Os administradores podem exibir todas as transações para todos os usuários, desde que não tenham o nível de permissão somente leitura aplicado na área funcional **Gerenciamento de Versão**. Por exemplo, se o nível de permissão somente leitura e de permissão de atualização estiver definido para o administrador, ele não poderá ver as transações de outro usuário porque a permissão somente leitura terá precedência sobre a permissão de atualização.

## <a name="system-settings"></a>Configurações do sistema  
 Há uma configuração no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] que afeta se as transações são ou não registradas quando os registros são preparados. Esta configuração só afeta o SQL Server 2008 R2. É possível ajustar essa configuração no [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] ou diretamente na tabela Configurações do Sistema do banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obter mais informações, veja [Configurações do sistema &#40;Master Data Services&#41;](system-settings-master-data-services.md).  
  
 Ao importar dados nesta versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], você poderá especificar se deseja ou não registrar em log as transações ao iniciar o procedimento armazenado. Para obter mais informações, consulte [Preparando um procedimento armazenado &#40;Master Data Services&#41;](../../2014/master-data-services/staging-stored-procedure-master-data-services.md).  
  
## <a name="concurrency"></a>Simultaneidade  
 Se um valor de entidade específico for mostrado simultaneamente em mais de uma sessão do Explorer, as edições simultâneas do mesmo valor serão permitidas. As edições simultâneas não serão detectadas automaticamente pelo MDS. Isso pode ocorrer quando vários usuários utilizarem o MDS Explorer no navegador da Web de várias sessões como, por exemplo, de vários computadores, várias guias ou janelas de navegador ou várias contas de usuário.  
  
 Mais de um usuário pode atualizar os mesmos valores de entidade sem erro apesar das transações habilitadas. Normalmente, a última edição do valor em determinado período terá precedência. O conflito de edição duplicada pode ser observado manualmente no histórico de transação e pode ser revertido manualmente pelo administrador. O histórico de transações mostrará as transações individuais para o **Valor anterior** e o **Novo valor** do atributo em questão de cada sessão, mas não resolverá o conflito automaticamente quando vários **Novos Valores** existirem para o mesmo valor antigo.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Desfazer uma ação por meio de reversão de uma transação (somente administradores).|[Inverter uma transação &#40;Master Data Services&#41;](../../2014/master-data-services/reverse-a-transaction-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)  
  
-   [Anotações &#40;Master Data Services&#41;](../../2014/master-data-services/annotations-master-data-services.md)  
  
  
