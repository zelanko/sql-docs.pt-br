---
title: 'Como: executar o Assistente para análise do Supervisor de atualização | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5ff92f0bb0cbf15e61895307d799415639a89eab
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120059"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>Como executar o Assistente para Análise do Supervisor de Atualização
  Você inicia o Assistente para Análise do Supervisor de Atualização na página inicial do Supervisor de Atualização. Este tópico descreve como executar o Assistente para Análise do Supervisor de Atualização.  
  
> [!IMPORTANT]  
>  Quando você executa o Assistente para Análise do Supervisor de Atualização, o Supervisor de Atualização salva os relatórios na pasta de relatórios padrão. Entretanto, o visualizador de relatórios exibe apenas os cinco relatórios mais recentes salvos. O local padrão para os relatórios é Meus documentos\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Advisor\110\Reports atualização.  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>Para executar o Assistente de análise do Supervisor de atualização  
  
1.  Na página inicial do Supervisor de atualização, clique em **Iniciar Assistente de análise Supervisor de atualização**.  
  
2.  No  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes** página, digite o nome do servidor a ser verificado no **nome do servidor** caixa e, em seguida, clique em **detectar**. Use as políticas a seguir para o nome de servidor:  
  
    -   Para verificar instâncias não clusterizadas, digite o nome do computador.  
  
    -   Para verificar instâncias clusterizadas, digite o nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] virtual.  
  
    -   Para verificar componentes não clusterizados que estão instalados em um nó de um cluster, digite o nome do nó.  
  
    > [!WARNING]  
    >  O Supervisor de Atualização não oferece suporte à conexão a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não é definida para usar a porta padrão (1433) para conexões de cliente. Se você desejar se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não usa a porta padrão (1433), crie um alias usando o endereço IP e a porta. Para obter mais informações sobre como configurar protocolos de cliente e criar um alias para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instâncias, consulte [configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md).  
    >   
    >  Se você não tem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador no qual você está executando o Supervisor de atualização, clique em **iniciar**e, em seguida, execute `cliconfg`. Isso abre o  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client Network Utility** caixa de diálogo. Use o **Alias** guia para criar o alias.  
  
3.  Examine a lista de componentes detectados, modifique as seleções conforme necessário e, em seguida, clique em **próximo**.  
  
4.  Sobre o **parâmetros de Conexão** , selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você deseja verificar, selecione o método de autenticação e, se necessário, insira as informações de nome e a senha do usuário e, em seguida, clique em **Avançar**.  
  
     O nome de instância padrão é MSSQLSERVER.  
  
5.  No caso dos componentes selecionados, digite as informações solicitadas. Para obter mais informações sobre caixas de diálogo individuais, consulte [Atualizar referência de Interface de usuário do Orientador de](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
6.  Sobre o **Confirmar configurações do Supervisor de atualização** , examine as informações que você inseriu. Você pode selecionar **enviar relatórios à [!INCLUDE[msCoName](../../includes/msconame-md.md)]**  se você deseja enviar o relatório de atualização. Você também pode visualizar a política de privacidade.  
  
7.  Clique em **executar** para analisar a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
8.  Quando a análise for concluída, clique em **Iniciar relatório** para exibir os problemas de atualização detectados.  
  
## <a name="see-also"></a>Consulte também  
 [Como: iniciar o Supervisor de atualização](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Executando o Supervisor de atualização &#40;Interface do usuário&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  