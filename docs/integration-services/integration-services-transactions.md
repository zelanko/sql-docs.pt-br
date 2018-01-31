---
title: "Transações do Integration Services | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- containers [Integration Services], transactions
- transactions [Integration Services], about transactions in packages
- tasks [Integration Services], transactions
- transactions [Integration Services]
ms.assetid: 3c78bb26-ddce-4831-a5f8-09d4f4fd53cc
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 83125af2f2f85c825aae5b594767fa421af2a656
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="integration-services-transactions"></a>Transações do Integration Services
  Os pacotes usam transações para associar as ações do banco de dados realizadas pelas tarefas em unidades atômicas e, ao fazer isso, a integridade dos dados é mantida. Todos os tipos de contêineres do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , pacotes, o Loop For, Loop Foreach, contêineres de Sequência, e os hosts de tarefas que encapsulam cada tarefa, podem ser configurados para usar transações. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] fornece três opções para configurar transações: **Sem Suporte**, **Há Suporte**e **Necessário**.  
  
-   **Necessário** indica que o contêiner inicia uma transação, a menos que uma já tenha sido iniciada por seu contêiner pai. Se uma transação já existir, o contêiner se unirá à transação. Por exemplo, se um pacote que não está configurado para dar suporte a transações incluísse um contêiner Sequência que usa a opção **Necessário** , o contêiner iniciaria sua própria transação. Se o pacote fosse configurado para usar a opção **Necessário** , o contêiner Sequência se uniria à transação do pacote.  
  
-   **Há Suporte** indica que o contêiner não inicia uma transação, mas se une a qualquer transação iniciada por seu contêiner pai. Por exemplo, se um pacote com quatro tarefas Executar SQL iniciar uma transação e todas as quatro tarefas usarem a opção **Há Suporte** , as atualizações de banco de dados realizadas pelas tarefas Executar SQL serão revertidas se qualquer tarefa falhar. Se o pacote não iniciar uma transação, as quatro tarefas Executar SQL não serão associadas por uma transação e nenhuma atualização de banco de dados, exceto as realizadas pela tarefa que falhou, será revertida.  
  
-   **Sem Suporte** indica que o contêiner não inicia uma transação ou se une a uma transação existente. Uma transação iniciada por um contêiner pai não afeta contêineres filhos que foram configurados para não suportar transações. Por exemplo, se um pacote for configurado para iniciar uma transação e um contêiner Loop For no pacote usar a opção **Sem Suporte** , nenhuma das tarefas no Loop For poderão ser revertidas se falharem.  
  
 Você configura transações definindo a propriedade TransactionOption no contêiner. É possível definir essa propriedade na janela **Propriedades** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]ou definir a propriedade programaticamente.  
  
> [!NOTE]  
>  A propriedade **TransactionOption** influencia a aplicação ou não do valor da propriedade **IsolationLevel** solicitada por um contêiner. Para obter mais informações, consulte a descrição da propriedade **IsolationLevel** no tópico [Definir propriedades do pacote](../integration-services/set-package-properties.md).  
  
## <a name="configure-a-package-to-use-transactions"></a>Configurar um pacote para usar transações
Quando você configura um pacote para usar transações, há duas opções:  
  
-   Ter uma única transação para o pacote. Nesse caso, é o próprio pacote que *inicia* a transação, enquanto tarefas e contêineres individuais do pacote participam desta única transação.  
  
-   Ter várias transações no pacote. Nesse caso, o pacote dá suporte a transações, mas na verdade são as tarefas e os contêineres individuais do pacote que iniciam as transações.  
  
 Os procedimentos a seguir descrevem como configurar ambas as opções.  
  
### <a name="configure-a-package-to-use-a-single-transaction"></a>Configurar um pacote para usar uma única transação  
 Nesta opção, o pacote propriamente dito inicia uma única transação. Para configurar o pacote para iniciar a transação, defina a propriedade TransactionOption do pacote como **Required**.  
  
 Em seguida, inscreva as tarefas e os contêineres específicos desta única transação. Para inscrever uma tarefa ou um contêiner em uma transação, defina a propriedade TransactionOption da tarefa ou do contêiner como **Com Suporte**.  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote o qual você deseja configurar para usar uma transação.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de controle e clique em **Propriedades**.  
  
5.  Na janela **Propriedades** , defina a propriedade TransactionOption como **Required**.  
  
6.  Na superfície de design da guia **Fluxo de Controle** , clique com o botão direito do mouse na tarefa ou no contêiner que deseja inserir na transação e clique em **Propriedades**.  
  
7.  Na janela **Propriedades** , defina a propriedade TransactionOption como **Com Suporte**.  
  
    > [!NOTE]  
    >  Para inscrever uma conexão em uma transação, inscreva as tarefas que usam a conexão na transação. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
8.  Repita as etapas 6 e 7 para cada tarefa e contêiner que você deseja inscrever na transação.  
  
### <a name="configure-a-package-to-use-multiple-transactions"></a>Configurar um pacote para usar transações múltiplas  
 Nesta opção, o próprio pacote dá suporte a transações, mas não inicia uma transação. Para configurar o pacote para dar suporte a transações, defina a propriedade TransactionOption do pacote como **Com Suporte**.  
  
 Em seguida, configure as tarefas e os contêineres desejados do pacote para iniciar ou participar de transações. Para configurar uma tarefa ou um contêiner para iniciar uma transação, defina a propriedade TransactionOption da tarefa ou do contêiner como **Required**.   
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote a ser configurado para usar transações.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de controle e clique em **Propriedades**.  
  
5.  Na janela **Propriedades** , defina a propriedade TransactionOption como **Com Suporte**.  
  
    > [!NOTE]  
    >  O pacote suporta transações, mas as transações são iniciadas por tarefa ou contêineres no pacote.  
  
6.  Na superfície de design da guia **Fluxo de Controle** , clique com o botão direito do mouse na tarefa ou no contêiner no pacote no qual deseja iniciar uma transação e clique em **Propriedades**.  
  
7.  Na janela **Propriedades** , defina a propriedade TransactionOption como **Required**.  
  
8.  Se a transação for iniciada por um contêiner, clique com o botão direito do mouse na tarefa ou no contêiner que deseja inserir na transação e clique em **Propriedades**.  
  
9. Na janela **Propriedades** , defina a propriedade TransactionOption como **Com Suporte**.  
  
    > [!NOTE]  
    >  Para inscrever uma conexão em uma transação, inscreva as tarefas que usam a conexão na transação. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
10. Repita as etapas de 6 a 9 para cada tarefa e contêiner que iniciam uma transação.  

## <a name="multiple-transactions-in-a-package"></a>Transações múltiplas em um pacote
É possível que um pacote inclua transações não relacionadas em um pacote [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . A qualquer hora que um contêiner no meio de uma hierarquia de contêineres aninhada não oferecer suporte a transações, os contêineres acima ou abaixo da mesma na hierarquia começa a separar as transações, se elas estiverem configuradas para oferecem suporte às transações. As transações confirmam ou revertem na ordem da tarefa interna na hierarquia de contêineres aninhados para o pacote. Entretanto, depois que a transação interna é confirmada, ela não será revertida se uma transação externa for anulada.  
  
### <a name="example-of-multiple-transactions-in-a-package"></a>Exemplo de transações múltiplas em um pacote 
 Por exemplo, um pacote tem um contêiner de Sequência que mantém dois contêineres Loop Foreach, e cada contêiner inclui duas tarefas Executar SQL. O contêiner Sequência oferece suporte a transações, os contêineres Loop Foreach não oferecem e as tarefas Executar SQL oferecem. Nesse exemplo, cada tarefa Executar SQL começaria sua própria transação e não reverteria se a transação da tarefa de Sequência fosse cancelada.  
  
 As propriedades TransactionOption do contêiner Sequência, do contêiner Loop Foreach e das tarefas Executar SQL são definidas da seguinte maneira:  
  
-   As propriedades TransactionOption do contêiner de Sequência está definida como **Obrigatória**.  
  
-   As propriedades TransactionOption dos contêineres Loop Foreach são definidas como **NotSupported**.  
  
-   As propriedades TransactionOption das tarefas Executar SQL são definidas como **Obrigatória**.  
  
 O diagrama a seguir mostra as cinco transações não relacionadas no pacote. Uma transação é iniciada pelo contêiner de Sequência e quatro transações são iniciadas pelas tarefas Executar SQL.  
  
 ![Implementação de transações múltiplas](../integration-services/media/mw-dts-trans2.gif "Implementation of multiple transactions")  
 
## <a name="inherited-transactions"></a>Transações herdadas
 Um pacote pode executar outro pacote usando a tarefa Executar Pacote. O pacote filho, que é o pacote executado pela tarefa Executar Pacote, pode criar sua própria transação de pacote ou pode herdar a transação do pacote pai.  
  
 Um pacote filho herda a transação do pacote pai se ambos os itens a seguir forem verdadeiros:  
  
-   O pacote é invocado por uma tarefa Executar Pacote.  
  
-   A tarefa Executar Pacote que invoca o pacote também tenha unido a transação de pacote pai.  
  
 Os contêineres e tarefas no pacote filho não podem unir-se à transação de pacote pai, a menos que o próprio pacote filho seja unido na transação.  
  
### <a name="example-of-inherited-transactions"></a>Exemplo de transações herdadas  
 No diagrama a seguir, há três pacotes que usam transações. Cada pacote contém múltiplas tarefas. Para enfatizar o comportamento das transações, só serão mostradas as tarefas Executar Pacote. O pacote A executa os pacotes B e C. Por sua vez, o pacote B executa os pacotes D e E, e o pacote C executa o pacote F.  
  
 Os pacotes e tarefas têm os seguintes atributos de transação:  
  
-   **TransactionOption** é definida como **Required** nos pacotes A e C  
  
-   **TransactionOption** é definida como **Com Suporte** nos pacotes B e D, e nas tarefas Executar Pacote B, Executar Pacote C e Executar Pacote F.  
  
-   **TransactionOption** é definida como **NotSupported** no pacote E e nas tarefas Executar Pacote C e Executar Pacote E.  
  
 ![Fluxo de transações herdadas](../integration-services/media/mw-dts-executepack.gif "Flow of inherited transactions")  
  
 Só pacotes B, D e F podem herdar transações de seus pacotes pai.  
  
 Pacotes B e D herdam a transação que foi iniciada pelo pacote A.  
  
 Pacote F herda a transação que foi iniciada pelo pacote C.  
  
 Pacotes A e C controlam suas próprias transações.  
  
 Pacote E não usa transações.  
 
  
## <a name="external-resources"></a>Recursos externos  
  
-   Entrada de blog, [How to Use Transactions in SQL Server Integration Services SSIS (em inglês)](http://go.microsoft.com/fwlink/?LinkId=157783), em www.mssqltips.com  
  
## <a name="see-also"></a>Consulte Também  
 [Transações herdadas](http://msdn.microsoft.com/library/90db5564-d41e-4cfe-8c9e-4e68d41eff1c)   
 [Transações múltiplas](http://msdn.microsoft.com/library/c3664a94-be89-40c0-a3a0-84b74a7fedbe)  
  
  
