---
title: Configurar um pacote para usar transações | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- transactions [Integration Services], configuring packages to use
ms.assetid: 8bf14957-27b4-456b-81d9-e1a0e0ca94b7
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 9d16473832d321e252753fa79e8b3178f2c2dcf6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921912"
---
# <a name="configure-a-package-to-use-transactions"></a>Configurar um pacote para usar transações
  Quando você configura um pacote para usar transações, há duas opções:  
  
-   Ter uma única transação para o pacote. Nesse caso, é o próprio pacote que *inicia* a transação, enquanto tarefas e contêineres individuais do pacote participam desta única transação.  
  
-   Ter várias transações no pacote. Nesse caso, o pacote dá suporte a transações, mas na verdade são as tarefas e os contêineres individuais do pacote que iniciam as transações.  
  
 Os procedimentos a seguir descrevem como configurar ambas as opções.  
  
## <a name="configuring-a-single-transaction"></a>Configurando uma única transação  
 Nesta opção, o pacote propriamente dito inicia uma única transação. Configure o pacote para iniciar essa transação definindo a propriedade TransactionOption do pacote como `Required` .  
  
 Em seguida, inscreva as tarefas e os contêineres específicos desta única transação. Para inscrever uma tarefa ou um contêiner em uma transação, defina a propriedade TransactionOption da tarefa ou do contêiner como `Supported` .  
  
#### <a name="to-configure-a-package-to-use-a-single-transaction"></a>Para configurar um pacote para usar uma única transação  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote o qual você deseja configurar para usar uma transação.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de controle e clique em **Propriedades**.  
  
5.  Na janela **Propriedades** , defina a propriedade TransactionOption como `Required` .  
  
6.  Na superfície de design da guia **Fluxo de Controle** , clique com o botão direito do mouse na tarefa ou no contêiner que deseja inserir na transação e clique em **Propriedades**.  
  
7.  Na janela **Propriedades** , defina a propriedade TransactionOption como `Supported` .  
  
    > [!NOTE]  
    >  Para inscrever uma conexão em uma transação, inscreva as tarefas que usam a conexão na transação. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](connection-manager/integration-services-ssis-connections.md).  
  
8.  Repita as etapas 6 e 7 para cada tarefa e contêiner que você deseja inscrever na transação.  
  
## <a name="configuring-multiple-transactions"></a>Configurando várias transações  
 Nesta opção, o próprio pacote dá suporte a transações, mas não inicia uma transação. Configure o pacote para dar suporte a transações definindo a propriedade TransactionOption do pacote como `Supported` .  
  
 Em seguida, configure as tarefas e os contêineres desejados do pacote para iniciar ou participar de transações. Para configurar uma tarefa ou um contêiner para iniciar uma transação, defina a propriedade TransactionOption da tarefa ou do contêiner como `Required` .  
  
#### <a name="to-configure-a-package-to-use-multiple-transactions"></a>Configurar um pacote para usar várias transações  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote a ser configurado para usar transações.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de controle e clique em **Propriedades**.  
  
5.  Na janela **Propriedades** , defina a propriedade TransactionOption como `Supported` .  
  
    > [!NOTE]  
    >  O pacote suporta transações, mas as transações são iniciadas por tarefa ou contêineres no pacote.  
  
6.  Na superfície de design da guia **Fluxo de Controle** , clique com o botão direito do mouse na tarefa ou no contêiner no pacote no qual deseja iniciar uma transação e clique em **Propriedades**.  
  
7.  Na janela **Propriedades** , defina a propriedade TransactionOption como `Required` .  
  
8.  Se a transação for iniciada por um contêiner, clique com o botão direito do mouse na tarefa ou no contêiner que deseja inserir na transação e clique em **Propriedades**.  
  
9. Na janela **Propriedades** , defina a propriedade TransactionOption como `Supported` .  
  
    > [!NOTE]  
    >  Para inscrever uma conexão em uma transação, inscreva as tarefas que usam a conexão na transação. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](connection-manager/integration-services-ssis-connections.md).  
  
10. Repita as etapas de 6 a 9 para cada tarefa e contêiner que iniciam uma transação.  
  
## <a name="see-also"></a>Consulte Também  
 [Transações do Integration Services](integration-services-transactions.md)  
  
  
