---
title: Resource Governor | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, overview
- Resource Governor
ms.assetid: 2bc89b66-e801-45ba-b30d-8ed197052212
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c7bbd2ba4ed132f3e1a795f72667c34f764c0d30
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="resource-governor"></a>Administrador de Recursos
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resource Governor é um recurso que você pode usar para gerenciar a carga de trabalho e o consumo de recursos do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O Administrador de Recursos permite que você especifique os limites de quantidade de CPU, E/S física e memória que as solicitações recebidas de aplicativos podem usar.  
  
## <a name="benefits-of-resource-governor"></a>Benefícios do Administrador de Recursos  
 O Administrador de Recursos permite gerenciar cargas de trabalho e recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificando limites de consumo de recursos por solicitações de entrada. No contexto do Administrador de Recursos, carga de trabalho é um conjunto de consultas ou solicitações de tamanho similar que podem e devem, ser tratadas como uma única entidade. Não se trata de um requisito, mas quanto mais uniforme for o padrão de uso dos recursos de uma carga de trabalho, maior a probabilidade de obter benefícios derivados do Administrador de Recursos. Limites de recurso podem ser reconfigurados em tempo real, com impacto mínimo sobre as cargas de trabalho que se encontram em execução.  
  
 Em um ambiente com várias cargas de trabalho distintas presentes no mesmo servidor, o Administrador de Recursos permite diferenciá-las e alocar recursos compartilhados conforme forem solicitados, segundo os limites especificados. Esses recursos são CPU, E/S física e memória.  
  
 Ao usar o Administrador de Recursos, você pode:  
  
-   Fornecer isolamento de multilocatário e de recurso em instâncias únicas do SQL Server que atendem várias cargas de trabalho cliente. Ou seja, você pode dividir os recursos disponíveis em um servidor entre as cargas de trabalho e minimizar os problemas que podem ocorrer quando as cargas de trabalho disputam os recursos.  
  
-   Forneça desempenho e SLAs de suporte previsíveis para locatários de cargas de trabalho em um ambiente de várias carga de trabalho e vários usuários.  
  
-   Isole e limite as consultas sem controle ou limite os recursos de E/S para operações como DBCC CHECKDB que pode saturar o subsistema de E/S e afetar negativamente outras cargas de trabalho.  
  
-   Adicione o controle refinado de recursos para estornos de uso de recurso e forneça a cobrança previsível para consumidores dos recursos do servidor.  
  
## <a name="resource-governor-constraints"></a>Restrições do Administrador de Recursos  
 Essa versão do Administrador de Recursos possui as seguintes restrições:  
  
-   O gerenciamento de recursos se limita ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. O Administrador de Recursos não pode ser usado para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]e o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Não há monitoramento ou gerenciamento de carga de trabalho entre instâncias do SQL Server.  
  
-   O Administrador de Recursos pode gerenciar cargas de trabalho OLTP, mas esses tipos de consulta, normalmente de duração bastante curta, nem sempre ficam na CPU o suficiente para a aplicação de controles de largura de banda. Isso pode distorcer as estatísticas retornadas quanto à porcentagem de uso da CPU.  
  
-   A capacidade de administrar E/S física aplica-se apenas a operações do usuário e não a tarefas do sistema. As tarefas do sistema incluem operações de gravação no log de transações e operações de E/S do Gravador Lento. O Administrador de Recursos se aplica basicamente às operações de leitura do usuário, pois a maioria das operações de gravação normalmente é executada por tarefas do sistema.  
  
-   Você não pode definir limites de E/S no pool de recursos interno.  
  
## <a name="resource-concepts"></a>Conceitos de recurso  
 Os três conceitos a seguir são fundamentais para compreensão e uso do Administrador de Recursos:  
  
-   **Pools de recursos.** O pool de recursos representa os recursos físicos do servidor. É possível pensar no pool como uma instância virtual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dentro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Dois pools de recursos (interno e padrão) são criados quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado. O Administrador de Recursos também oferece suporte a pools de recursos definidos pelo usuário. Para obter mais informações, consulte [Pool de recursos do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
-   **Grupos de carga de trabalho.** Um grupo de carga de trabalho funciona como um contêiner para as solicitações de sessão que têm critérios de classificação similares. Uma carga de trabalho permite o monitoramento de agregação de sessões e define políticas para as sessões. Cada grupo de cargas de trabalho está em um pool de recursos. Dois grupos de carga de trabalho (interno e padrão) são criados e mapeados para os pools de recursos correspondentes quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado. O Administrador de Recursos também oferece suporte a grupos de carga de trabalho definidos pelo usuário. Para obter mais informações, consulte [Grupos de carga de trabalho do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md).  
  
-   **Classificação.** O processo de Classificação atribui sessões de entrada a um grupo de cargas de trabalho baseado nas características da sessão. Você pode personalizar a lógica de classificação gravando uma função definida pelo usuário, chamado de função de classificador. O Administrador de Recursos também oferece suporte à função de classificação definida pelo usuário para implementar as regras de classificação. Para obter mais informações, consulte [Função de classificação do Administrador de Recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md).  
  
> [!NOTE]  
>  O Administrador de Recursos não impõe nenhum controle em uma conexão de administrador dedicada (DAC). Não é necessário classificar as consultas de DAC que executam no grupo de carga de trabalho interno e no pool de recursos.  
  
 No contexto do Administrador de Recursos, é possível tratar os conceitos anteriores como componentes. A ilustração a seguir mostra esses componentes e suas relações conforme surgem no ambiente do mecanismo de banco de dados. Do ponto de vista do processamento, o fluxo simplificado é o seguinte:  
  
-   Há uma conexão de entrada para uma sessão (Sessão 1 de *n*).  
  
-   A sessão é classificada (Classificação).  
  
-   A carga de trabalho de sessão é roteada para um grupo de carga de trabalho, por exemplo, Grupo 4.  
  
-   O grupo de carga de trabalho usa o pool de recursos ao qual está associado, por exemplo, Pool 2.  
  
-   O pool de recursos fornece e limita os recursos requeridos pelo aplicativo, por exemplo, Aplicativo 3.  
  
 ![Componentes funcionais do Resource Governor](../../relational-databases/resource-governor/media/rg-basic-funct-components.gif "Componentes funcionais do Resource Governor")  
  
## <a name="resource-governor-tasks"></a>Tarefas do Administrador de Recursos  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como habilitar o Administrador de Recursos.|[Habilitar Administrador de Recursos](../../relational-databases/resource-governor/enable-resource-governor.md)|  
|Descreve como desabilitar o Administrador de Recursos.|[Desabilitar Administrador de Recursos](../../relational-databases/resource-governor/disable-resource-governor.md)|  
|Descreve como criar, alterar e descartar um pool de recursos.|[Pool de recursos do Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)|  
|Descreve como criar, alterar, mover e descarregar um grupo de cargas de trabalho.|[Grupos de carga de trabalho do Resource Governor](../../relational-databases/resource-governor/resource-governor-workload-group.md)|  
|Descreve como criar e testar uma função de classificação definida pelo usuário.|[Função do classificador do Resource Governor](../../relational-databases/resource-governor/resource-governor-classifier-function.md)|  
|Descreve como configurar o Administrador de Recursos usando um modelo.|[Configurar o administrador de recursos usando um modelo](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)|  
|Descreve como exibir as propriedades do Administrador de Recursos.|[Exibir Propriedades do Resource Governor](../../relational-databases/resource-governor/view-resource-governor-properties.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Instâncias do mecanismo de banco de dados &#40;SQL Server&#41;](../../database-engine/configure-windows/database-engine-instances-sql-server.md)  
  
  

