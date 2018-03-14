---
title: "Conceitos de programação de replicação | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- replication [SQL Server], planning
- programming [SQL Server replication], planning
- programming [SQL Server replication]
ms.assetid: 2cd846e7-5bf3-4144-8772-703c4f439a2a
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b11b26f7cdfbdedfe24fa8ba45eee236792b876
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="replication-programming-concepts"></a>Conceitos de programação de replicação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Antes de desenvolver um aplicativo que utilize funcionalidades de replicação, siga estas etapas de planejamento gerais:  
  
1.  Defina a sua topologia de replicação.  
  
2.  Defina a funcionalidade do aplicativo.  
  
3.  Planeje a segurança.  
  
4.  Escolha um ambiente de desenvolvimento.  
  
5.  Escolha a interface de programação de replicação apropriada.  
  
 O restante deste tópico descreverá essas etapas em mais detalhes. Para ajudar ilustrar o processo de planejamento, foi incluído um exemplo.  
  
## <a name="defining-the-replication-topology"></a>Definindo a topologia de replicação  
 A primeira etapa da programação da replicação é definir a topologia de replicação para o seu aplicativo. Se você estiver escrevendo um aplicativo que usará uma topologia de replicação existente, como um aplicativo cliente que acessa dados em um assinante existente, prossiga para a próxima etapa.  
  
> [!NOTE]  
>  Em alguns casos, implantar a topologia de replicação será o único propósito do aplicativo.  
  
 A topologia de replicação definida dependerá de muitos fatores, inclusive os seguintes:  
  
-   Se os dados replicados precisam ou não ser atualizados, e por quem.  
  
-   As necessidades da distribuição de dados em relação à consistência, à autonomia e à latência.  
  
-   O ambiente de replicação, incluindo usuários comerciais, infraestrutura técnica, rede e segurança e características de dados.  
  
-   Os tipos de replicação e as opções de replicação.  
  
-   As topologias de replicação e como elas se alinham aos tipos de replicação.  
  
 Se você não está familiarizado com replicação do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [Tipos de replicação](../../../relational-databases/replication/types-of-replication.md).  
  
## <a name="defining-application-functionality"></a>Definindo a funcionalidade do aplicativo  
 Após a definição da topologia de replicação, decida quais serão as funcionalidades oferecidas pelo seu aplicativo. Essas funcionalidades poderão variar de um script que sincroniza uma assinatura até um aplicativo com uma interface do usuário para a configuração da replicação. A replicação oferece suporte às seguintes tarefas de programação gerais:  
  
-   Configuração da replicação.  
  
-   Sincronização de Assinantes.  
  
-   Manutenção de uma topologia de replicação.  
  
-   Monitoramento de uma topologia de replicação.  
  
-   Solução de problemas de replicação.  
  
 Também é comum estender o seu aplicativo combinando funcionalidades de replicação com outras funcionalidades oferecidas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A tabela a seguir realça algumas das funcionalidades estendidas que podem ser oferecidas em seu aplicativo de replicação.  
  
|Funcionalidade|Exemplo|  
|-------------------|-------------|  
|Administração de servidor que usa o SMO do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]|Um aplicativo que permite a um administrador anexar e configurar um banco de dados como um Publicador em uma topologia de replicação.|  
|Acesso a dados usando o ADO.NET|Um aplicativo que permite aos usuários acessar e alterar programaticamente dados de venda replicados em um banco de dados Assinante local em modo offline e então conectar-se a uma assinatura pull e sincronizar com ela clicando em um botão.|  
  
## <a name="planning-for-security"></a>Planejando a segurança  
 A segurança é importante em qualquer aplicativo e se planejamento deveria ser concluído antes de qualquer código ser escrito. A segurança do aplicativo pode ser dividida em três partes principais: proteção do banco de dados, proteção da replicação e escrita de código seguro.  
  
 Os tópicos a seguir oferecem informações sobre segurança:  
  
-   [Segurança e proteção &#40;Replicação&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
-   [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
## <a name="choosing-a-development-environment"></a>Escolhendo um ambiente de desenvolvimento  
 Durante o desenvolvimento de um aplicativo de replicação, existem três ambientes de desenvolvimento básicos a se considerar. Cada ambiente de desenvolvimento tem acesso às mesmas funcionalidades de replicação, com algumas exceções. Os aplicativos de replicação podem ser desenvolvidos em cada um dos ambientes a seguir.  
  
-   **Código gerenciado**  
  
     Ambiente de desenvolvimento orientado a objeto que aproveita os benefícios da programação [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] e do CLR (common language runtime) .NET. O código gerenciado é o ambiente de programação indicado para o desenvolvimento de .NET e de aplicativos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. As interfaces de replicação gerenciadas permitem a programação de administração de replicação de uma forma orientada a objeto sem que seja preciso conhecer o [!INCLUDE[tsql](../../../includes/tsql-md.md)], e também oferece algumas funcionalidades de retorno de chamada durante a execução de agentes de replicação não disponíveis em scripts. O código gerenciado é o melhor ambiente para o desenvolvimento de componentes e de aplicativos de interface do usuário reutilizáveis.  
  
-   **Script**  
  
     Aplicativos simples que executam uma série de comandos, além de quaisquer procedimentos armazenados do sistema de replicação presentes em scripts ou comandos [!INCLUDE[tsql](../../../includes/tsql-md.md)] de arquivos em lotes. Embora você possa executar scripts em um ambiente gerenciado usando o provedor gerenciado em processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a mesma funcionalidade pode ser obtida com interfaces de replicação, que também oferecem funcionalidades de retorno de chamada. A geração de scripts é o melhor ambiente para a execução de tarefas que só serão executadas algumas vezes e onde as funcionalidades de retorno de chamada não serão necessárias, como na instalação de um servidor de replicação.  
  
-   **Código nativo**  
  
     Ambiente de desenvolvimento orientado a objeto que utiliza acesso direto ao sistema ou a objetos COM como o código que não é gerenciado pelo CLR. As interfaces de replicação do código nativo não estão disponíveis ou foram descontinuadas. Para obter mais informações, consulte [Recursos preteridos na Replicação do SQL Server](../../../relational-databases/replication/deprecated-features-in-sql-server-replication.md) ou [Compatibilidade com versões anteriores da replicação](../../../relational-databases/replication/replication-backward-compatibility.md).  
  
## <a name="choose-the-appropriate-replication-programming-interface"></a>Escolha a interface de programação de replicação apropriada  
 A última etapa de planejamento é escolher a interface de programação de replicação apropriada que implementará a funcionalidade de replicação desejada para o ambiente de desenvolvimento escolhido. A tabela a seguir mostra as interfaces de programação de replicação disponíveis.  
  
|Interface|Ambiente|Usos|  
|---------------|-----------------|----------|  
|[Conceitos de objetos de gerenciamento de replicação](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)|Código gerenciado|Administração, monitoramento e sincronização.|  
|<xref:Microsoft.SqlServer.Replication>|Código gerenciado|Sincronização.|  
|<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|Código gerenciado|Criação de manipuladores de lógica de negócios para integrar lógica personalizada ao processo de sincronização de mesclagem.|  
|[Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|Script|Administração e monitoramento.|  
|[Conceitos dos executáveis do Replication Agent](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)|Script|Sincronização.|  
  
## <a name="example"></a>Exemplo  
 No [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)], os dados precisam ser publicados para 200 representantes de vendas de todo o mundo. Os representantes de venda viajam com muita frequência e precisam usar laptops ou PDAs (personal digital assistants) para alterar dados de clientes e para adicionar novos pedidos. As alterações terão de ser sincronizadas com o Publicador quando o representante de vendas conectar o laptop à rede.  
  
 Para este aplicativo, as etapas de planejamento poderiam ser as seguintes:  
  
1.  A topologia de replicação para este aplicativo já existe. No entanto, uma nova assinatura pull deverá ser criada no cliente. A publicação deve usar filtros parametrizados para replicar um conjunto de dados exclusivo para cada representante de vendas.  
  
2.  Além do acesso a dados típico exigido para um aplicativo de venda, este aplicativo deve permitir que os vendedores sincronizem a assinatura pull sob demanda clicando em um botão. Uma vez que o representante de vendas instalará e executará o aplicativo, também terá de ser capaz de configurar uma assinatura e de aplicar o instantâneo inicial no cliente. Opcionalmente, o aplicativo usará a infraestrutura fornecida pelo Windows para localizar a conectividade sem-fios e sincronizar a assinatura automaticamente quando uma conexão for detectada.  
  
3.  Siga todas as diretrizes de segurança para replicação, incluindo a utilização da Autenticação de Windows e de uma VPN (rede privada virtual) ao se conectar ao editor. Se estiver implementando a sincronização da Web, use uma conexão de protocolo SSL. Para obter mais informações, consulte [Configurar sincronização da Web](../../../relational-databases/replication/configure-web-synchronization.md).  
  
4.  Para tirar proveito dos recursos do [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], o aplicativo será desenvolvido usando uma linguagem de código gerenciado.  
  
5.  Com base nesses requisitos, a interface gerenciada do RMO (Replication Management Objects) pode oferecer toda a funcionalidade de replicação necessária para este aplicativo.  
  
 Esse cenário de exemplo foi implementado no aplicativo de exemplo AdventureWorks que pode ser baixado para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
  
