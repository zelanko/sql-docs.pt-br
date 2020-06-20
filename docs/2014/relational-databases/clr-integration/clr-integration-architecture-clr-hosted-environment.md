---
title: Ambiente hospedado do CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- type-safe code [CLR integration]
- UNSAFE permission set
- run-time environments [CLR integration]
- common language runtime [SQL Server], about CLR integration
- application domains [CLR integration]
- host protection attributes [CLR integration]
- managed code [SQL Server], common language runtime
- permission sets [CLR integration]
- reliability [CLR integration]
- SAFE permission set
- code access security [CLR integration]
- EXTERNAL_ACCESS permission set
- verifying type safety
- scalability [CLR integration]
- hosted environments [CLR integration]
- HPAs [CLR integration]
ms.assetid: d280d359-08f0-47b5-a07e-67dd2a58ad73
author: rothja
ms.author: jroth
ms.openlocfilehash: 11eae15e50c26c4abde212ef273d6ede63ffe30d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953859"
---
# <a name="clr-hosted-environment"></a>Ambiente hospedado de CLR
  O CLR (Common Language Runtime) do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework é um ambiente que executa várias linguagens de programação modernas, incluindo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C++. O CLR tem memória com coleta de lixo, threading preemptivo, serviços de metadados (reflexão de tipo), capacidade de verificação de código e segurança de acesso ao código. Ele usa metadados para localizar e carregar classes, distribuir as instâncias na memória, resolver invocações de métodos, gerar código nativo, impor a segurança e definir limites de contexto em tempo de execução.  
  
 O CLR e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] diferem como ambientes de tempo de execução pela forma como tratam memória, threads e sincronização. Este tópico descreve a forma na qual estes dois tempos de execução são integrados para que todos os recursos do sistema sejam gerenciados uniformemente. Este tópico também fala sobre a forma na qual a CAS (segurança de acesso do código) do CLR e a segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são integradas para fornecer um ambiente de execução confiável e seguro para o código do usuário.  
  
## <a name="basic-concepts-of-clr-architecture"></a>Conceitos básicos da arquitetura do CLR  
 No .NET Framework, um programador escreve o código em uma linguagem de alto nível que implementa uma classe definindo sua estrutura (por exemplo, os campos das propriedades da classe) e seus métodos. Alguns desses métodos podem ser funções estáticas. A compilação do programa produz um arquivo chamado assembly, que contém o código compilado na MSIL ([!INCLUDE[msCoName](../../../includes/msconame-md.md)] intermediate language) e um manifesto que contém todas as referências para assemblies dependentes.  
  
> [!NOTE]  
>  Os assemblies são um elemento vital na arquitetura do CLR. Eles são as unidades de empacotamento, implantação e controle de versão de código de aplicativo no .NET Framework. Usando assemblies, você pode implantar código de aplicativo no banco de dados e fornecer um modo uniforme de administrar, fazer backup e restaurar aplicativos de bancos de dados completos.  
  
 O manifesto do assembly contém metadados sobre o assembly, descrevendo todas as estruturas, campos, propriedades, classes, relacionamentos de herança, funções e métodos definidos no programa. O manifesto estabelece a identidade do assembly, especifica os arquivos que compõem a sua implementação, especifica os tipos e recursos que o compõem, mantém uma lista das dependências de tempo de compilação em outros assemblies e especifica o conjunto de permissões necessárias para que seja executado adequadamente. Estas informações são usadas em tempo de execução para resolver referências, impor a política de ligação da versão e validar a integridade dos assemblies carregados.  
  
 O .NET Framework dá suporte a atributos personalizados para anotar classes, propriedades, funções e métodos com informações adicionais que o aplicativo possa capturar em metadados. Todos os compiladores .NET Framework consomem essas anotações sem interpretação e as armazenam como metadados de assembly. Estas anotações podem ser examinadas da mesma forma que quaisquer outros metadados.  
  
 O código gerenciado é MSIL executado no CLR, em vez de diretamente pelo sistema operacional. Aplicativos de código gerenciado adquirem serviços de CLR, como coleta de lixo automática, verificação de tipo de tempo de execução e suporte de segurança. Estes serviços ajudam a fornecer uma plataforma uniforme, bem como comportamento independente de linguagem de aplicativos de código gerenciado.  
  
## <a name="design-goals-of-clr-integration"></a>Metas de design da integração de CLR  
 Quando o código de usuário é executado dentro do ambiente hospedado pelo CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (chamada de integração de CLR), aplicam-se as seguintes as metas de design:  
  
###### <a name="reliability-safety"></a>Confiabilidade (segurança)  
 O código do usuário não deve ter permissão para realizar operações que comprometam a integridade do processo do Mecanismo de banco de dados, como exibir uma mensagem em pop-up solicitando resposta do usuário ou sair do processo. Também não deve ser capaz substituir os buffers de memória ou as estruturas de dados internas do Mecanismo de banco de dados.  
  
###### <a name="scalability"></a>Escalabilidade  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o CLR têm modelos internos diferentes para agendamento e gerenciamento de memória. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte a um modelo de threading cooperativo, e não preemptivo, no qual os threads são executados de forma voluntária, periodicamente ou quando estão aguardando bloqueios ou E/S. O CLR dá suporte um modelo de threading preemptivo. Se o código do usuário que estiver sendo executado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puder chamar diretamente as primitivas de threading do sistema operacional, então ele não se integrará bem ao agendador de tarefas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e poderá degradar a escalabilidade do sistema. O CLR não faz distinção entre memória física e virtual, mas o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] gerencia diretamente a memória física e deve usar a memória física dentro de um limite configurável.  
  
 Os diferentes modelos de threading, agendamento e gerenciamento de memória são um desafio de integração para um RDBMS (sistema de gerenciamento de banco de dados relacional) que se dimensiona para dar suporte a milhares de sessões de usuário simultâneas. A arquitetura deve garantir que a escalabilidade do sistema não seja comprometida pelo código de usuário que chame diretamente APIs (application programming interfaces) para primitivas de threading, memória e sincronização.  
  
###### <a name="security"></a>Segurança  
 Código de usuário em execução no banco de dados deve seguir regras de autenticação e autorização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ao acessar objetos de banco de dados como tabelas e colunas. Além disso, os administradores de bancos de dados devem ter a capacidade de controlar o acesso aos recursos do sistema operacional, como arquivos e acesso à rede, do código de usuário em execução no banco de dados. Isto se torna importante à medida que as linguagens de programação gerenciadas (ao contrário de linguagens de programação não gerenciadas, como o Transact-SQL) fornecem APIs para acessar tais recursos. O sistema deve fornecer um modo seguro para que o código de usuário acesse os recursos da máquina fora do processo do [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Para obter mais informações, consulte [CLR Integration Security](security/clr-integration-security.md).  
  
###### <a name="performance"></a>Desempenho  
 Código de usuário gerenciado em execução no [!INCLUDE[ssDE](../../../includes/ssde-md.md)] deve ter desempenho computacional comparável ao mesmo código executado fora do servidor. O acesso ao banco de dados a partir de código do usuário gerenciado não é tão rápido quanto [!INCLUDE[tsql](../../../includes/tsql-md.md)] nativo. Para obter mais informações, consulte [desempenho da integração CLR](clr-integration-architecture-performance.md).  
  
## <a name="clr-services"></a>Serviços CLR  
 O CLR fornece vários serviços para ajudar atingir as metas de design da integração do CLR com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
###### <a name="type-safety-verification"></a>Verificação de segurança de tipo  
 Código fortemente tipado é um código que acessa as estruturas de memória somente de modos bem definidos. Por exemplo, dada uma referência de objeto válida, o código fortemente tipado pode acessar memória em offsets fixos, correspondentes a membros de campo reais. Entretanto, se o código acessar a memória em offsets arbitrários dentro ou fora do intervalo de memória que pertence ao objeto, então ele não será fortemente tipado. Quando os assemblies são carregados no CLR, antes de a MSIL ser compilada usando compilação JIT (just-in-time), o runtime executa uma fase de verificação que examina o código antes de determinar sua segurança de tipos. O código aprovado com êxito nesta verificação é chamado de código fortemente tipado verificável.  
  
###### <a name="application-domains"></a>Domínios de aplicativo  
 O CLR dá suporte à noção de domínios de aplicativo como zonas de execução dentro de um processo de host, onde assemblies de código gerenciado podem ser carregados e executados. O limite do domínio do aplicativo fornece isolamento entre assemblies. Os assemblies são isolados em termos de visibilidade de variáveis estáticas e membros de dados e de capacidade para chamar código dinamicamente. Domínios de aplicativo também são o mecanismo para carregar e descarregar código. O código só pode ser descarregado da memória através do descarregamento do domínio de aplicativo. Para obter mais informações, consulte [domínios de aplicativo e segurança de integração CLR](../../database-engine/dev-guide/application-domains-and-clr-integration-security.md).  
  
###### <a name="code-access-security-cas"></a>CAS (segurança de acesso ao código)  
 O sistema de segurança CLR sistema fornece um modo de controlar quais os tipos de código gerenciado de operações que podem ser executados, atribuindo permissões ao código. As permissões de acesso ao código são atribuídas com base na identidade do código (por exemplo, a assinatura do assembly ou a origem do código).  
  
 O CLR fornece uma política para todo o computador que pode ser definida pelo administrador do computador. Essa política define as concessões de permissão para qualquer código gerenciado em execução na máquina. Além disso, há uma política de segurança em nível de host que pode ser usada por hosts, como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], para especificar restrições adicionais em código gerenciado.  
  
 Se uma API gerenciada no .NET Framework expuser operações sobre recursos que são protegidas por uma permissão de acesso a código, a API solicitará essa permissão antes de acessar o recurso. Essa solicitação faz o sistema de segurança CLR ativar uma verificação abrangente de cada unidade de código (assembly) na pilha de chamadas. Somente se toda a cadeia de chamada tiver permissão, o acesso ao recurso será concedido.  
  
 Observe que não há suporte à capacidade de gerar código gerenciado dinamicamente, usando a API Reflection.Emit, dentro do ambiente hospedado pelo CLR no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esse código não teria as permissões de execução da CAS e, portanto, falharia em tempo de execução. Para obter mais informações, consulte [segurança de acesso ao código de integração CLR](security/clr-integration-code-access-security.md).  
  
###### <a name="host-protection-attributes-hpas"></a>HPAs (atributos de proteção de host)  
 O CLR fornece um mecanismo para anotar APIs gerenciadas que fazem parte do .NET Framework com determinados atributos que podem ser de interesse de um host do CLR. Exemplos de tais atributos incluem:  
  
-   SharedState, que indica se a API expõe a capacidade de criar ou gerenciar estado compartilhado (por exemplo, campos de classe estáticos).  
  
-   Synchronization, que indica se a API expõe a capacidade para executar sincronização entre threads.  
  
-   ExternalProcessMgmt, que indica se a API expõe um modo de controlar o processo de host.  
  
 Dados esses atributos, o host pode especificar uma lista de HPAs, como o atributo SharedState, que devem ser desabilitados no ambiente hospedado. Nesse caso, o CLR nega as tentativas do código de usuário de chamar APIs que são anotadas pelo HPAs na lista proibida. Para obter mais informações, consulte [atributos de proteção do host e programação de integração do CLR](../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
## <a name="how-sql-server-and-the-clr-work-together"></a>Como o SQL Server e o CLR trabalham juntos  
 Esta seção discute como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] integra os modelos de threading, agendamento, sincronização e gerenciamento de memória do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e do CLR. Em particular, esta seção examina a integração sob o ponto de vista das metas de escalabilidade, confiabilidade e segurança. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] atua essencialmente como o sistema operacional para o CLR quando este é hospedado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O CLR chama rotinas de baixo nível implementadas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para threading, agendamento e gerenciamento de memória. Elas são as mesmas primitivas que o restante do mecanismo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa. Esta abordagem fornece vários benefícios de escalabilidade, confiabilidade e segurança.  
  
###### <a name="scalability-common-threading-scheduling-and-synchronization"></a>Escalabilidade: Threading, agendamento e sincronização comuns  
 O CLR chama as APIs do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para criar threads, tanto para executar código de usuário quanto para seu próprio uso interno. Para fazer a sincronização de vários threads, o CLR chama objetos de sincronização do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Isto permite que o agendador [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para agende outras tarefas quando um thread estiver esperando um objeto de sincronização. Por exemplo, quando o CLR iniciar a coleta de lixo, todos os seus threads esperam a coleta de lixo terminar. Como os threads do CLR e os objetos de sincronização pelos quais eles estão esperando são conhecidos para o agendador do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode agendar threads que estão executando outras tarefas do banco de dados que não envolvem o CLR. Isto também permite que o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] detecte deadlocks que envolvem bloqueios tomados pelos objetos de sincronização CLR e utilize técnicas tradicionais para remoção de deadlock.  
  
 O código gerenciado é executado preventivamente no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O agendador do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem a capacidade de detectar e parar threads que não tenham sido executados durante um tempo significativo. A capacidade de conectar threads do CLR a threads do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] implica que o agendador do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode identificar threads “fugitivos” no CLR e gerenciar sua prioridade. Tais threads fugitivos são suspensos e devolvidos à fila. Os threads que são identificados repetidamente como fugitivos não recebem permissão de execução por um determinado período de tempo, para que outros trabalhos possam ser executados.  
  
> [!NOTE]  
>  Código gerenciado de execução longa que acessa dados ou aloca memória suficiente para disparar a coleta de lixo será executado automaticamente. Código gerenciado de execução longa que não acessa dados ou nem aloca memória gerenciada suficiente para disparar a coleta de lixo deve ser executado explicitamente, através da chamada da função System.Thread.Sleep() do .NET Framework.  
  
###### <a name="scalability-common-memory-management"></a>Escalabilidade: Gerenciamento de memória comum  
 O CLR chama primitivas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para alocar e desalocar sua memória. Como a memória usada pelo CLR é contabilizada no uso de memória total do sistema, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode permanecer dentro dos seus limites de memória configurados e garantir que o CLR e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] não compitam entre si pela memória. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também por rejeitar solicitações de memória do CLR quando a memória do sistema for limitada e solicitar ao CLR que reduza seu uso de memória quando outras tarefas precisarem de memória.  
  
###### <a name="reliability-application-domains-and-unrecoverable-exceptions"></a>Confiabilidade: Domínios de aplicativo e exceções irrecuperáveis  
 Quando o código gerenciado nas APIs do .NET Framework encontra exceções críticas, como memória insuficiente ou estouro da pilha, nem sempre é possível recuperar-se de tais falhas e garantir a semântica consistente e correta para sua implementação. Estas APIs geram uma exceção de anulação de thread em resposta a essas falhas.  
  
 Quando é feita hospedagem no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], essas anulações de thread são manipuladas da seguinte forma: o CLR detecta qualquer estado compartilhado no domínio do aplicativo no qual a anulação de thread ocorre. Ele faz isto verificando para a presença de objetos de sincronização. Se houver um estado compartilhado no domínio do aplicativo, então o próprio domínio do aplicativo será descarregado. A descarga do domínio do aplicativo para transações de banco de dados que estão em execução no momento, naquele domínio de aplicativo. Como a presença do estado compartilhado pode ampliar o impacto de tais exceções críticas para as sessões de usuário que não são aquela que está disparando a exceção, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o CLR tomaram medidas para reduzir a probabilidade de estado compartilhado. Para obter mais informações, consulte a documentação do .NET Framework.  
  
###### <a name="security-permission-sets"></a>Segurança: conjuntos de permissões  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite que os usuários especifiquem os requisitos de confiabilidade e segurança para o código implantado no banco de dados. Quando os assemblies são carregados no banco de dados, o autor do assembly pode especificar um dos três conjuntos de permissões para esse assembly: SAFE, EXTERNAL_ACCESS e UNSAFE.  
  
|||||  
|-|-|-|-|  
|Conjunto de permissões|SAFE|EXTERNAL_ACCESS|UNSAFE|  
|Segurança de Acesso do Código|Somente execução|Execução + acesso a recursos externos|Irrestrito|  
|Restrições do modelo de programação|Sim|Sim|Sem restrições|  
|Requisito de verificabilidade|Sim|Sim|Não|  
|Capacidade de chamar código nativo|Não|Não|Sim|  
  
 SAFE é o modo mais confiável e seguro, com restrições associadas ao modelo de programação permitido. Assemblies SAFE recebem permissão suficiente para executar, realizar cálculos e ter acesso ao banco de dados local. Assemblies SAFE precisam ser seguros do tipo verificável e não têm permissão para chamar código não gerenciado.  
  
 UNSAFE é para código altamente confiável que pode ser criado somente por administradores de bancos de dados. Este código confiável não tem nenhuma restrição de segurança de acesso a código e pode chamar código não gerenciado (nativo).  
  
 EXTERNAL_ACCESS fornece uma opção de segurança intermediária, permitindo que o código acesse recursos externos ao banco de dados, mas ainda tenha as garantias de confiabilidade de SAFE.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa a camada de políticas do CAS no nível de host para configurar uma política de host que conceda um dos três conjuntos de permissões com base no conjunto de permissões armazenado nos catálogos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Código gerenciado em execução dentro do banco de dados sempre obtém um desses conjuntos de permissão de acesso de código.  
  
### <a name="programming-model-restrictions"></a>Restrições do Modelo de Programação  
 O modelo de programação para código gerenciado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] envolve a codificação de funções, procedimentos e tipos que normalmente não exigem o uso do estado mantido entre várias invocações nem o compartilhamento do estado entre várias sessões de usuário. Além disso, conforme descrito anteriormente, a presença do estado compartilhado pode causar exceções críticas que afetam a escalabilidade e a confiabilidade do aplicativo.  
  
 Dadas essas considerações, desencorajamos o uso de variáveis estáticas e membros de dados estáticos de classes usado no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para assemblies SAFE e EXTERNAL_ACCESS, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] examina os metadados do assembly na ocasião CREATE ASSEMBLY e gerará uma falha na criação desses assemblies se encontrar o uso de membros e variáveis de dados estáticos.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também desabilita as chamadas às APIs do .NET Framework que são anotadas com os atributos de proteção do host `SharedState`, `Synchronization` e `ExternalProcessMgmt`. Isso impede que os assemblies SAFE e EXTERNAL_ACCESS chamem APIs que permitam compartilhar o estado, fazer sincronização e afetar a integridade do processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [restrições do modelo de programação de integração CLR](database-objects/clr-integration-programming-model-restrictions.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de integração CLR](security/clr-integration-security.md)   
 [Desempenho da integração CLR](clr-integration-architecture-performance.md)  
  
  
