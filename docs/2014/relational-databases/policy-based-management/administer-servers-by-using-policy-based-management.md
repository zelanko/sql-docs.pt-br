---
title: Administrar servidores com Gerenciamento Baseado em Políticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- facet See facets
- Declarative Management Framework See Policy-Based Management
- surface area configuration [SQL Server], Policy-Based Management
- Policy-Based Management
- facets [Policy-Based Management]
- Policy-Based Management, administering
- conditions [Policy-Based Management]
- facets [Policy-Based Management], about facets
- PolicyAdministratorRole role
ms.assetid: ef2a7b3b-614b-405d-a04a-2464a019df40
caps.latest.revision: 75
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 85dce54590cfb35286b6939ae9bffdc91f367fbe
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37264447"
---
# <a name="administer-servers-by-using-policy-based-management"></a>Administrar servidores com Gerenciamento Baseado em Políticas
  O Gerenciamento Baseado em Políticas é um sistema para gerenciar uma ou mais instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando os administradores de políticas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usam o Gerenciamento Baseado em Políticas, eles usam o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar políticas para gerenciar entidades no servidor, como as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], bancos de dados ou outros objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="benefits-of-policy-based-management"></a>Benefícios do Gerenciamento Baseado em Políticas  
 O Gerenciamento Baseado em Políticas é útil na solução dos problemas apresentados nos seguintes cenários:  
  
-   Uma política de empresa proíbe a habilitação do Database Mail ou do SQL Mail. Uma política é criada para verificar o estado do servidor desses dois recursos. Um administrador compara o estado do servidor com a política. Se o estado estiver fora de conformidade, o administrador escolherá o modo Configurar e a política providenciará a compatibilidade do estado do servidor.  
  
-   O banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] tem uma convenção de nomenclatura que requer que todos os procedimentos armazenados comecem com as letras AW_. Uma política é criada para impor essa política. Um administrador testa essa política e recebe uma lista de procedimentos armazenados que estão fora de conformidade. Se os procedimentos armazenados futuros não estiverem em conformidade com essa convenção de nomenclatura, haverá falha nas instruções de criação dos procedimentos armazenados.  
  
> [!NOTE]  
>  Esteja ciente que as políticas podem afetar como alguns recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionam. Por exemplo, a captura de dados de alterações e a replicação transacional usam uma tabela systranschemas que não possui um índice. Se você habilitar uma política em que todas as tabelas devam ter um índice, a imposição de conformidade da política causará falha nesses recursos.  
  
 As políticas são criadas e gerenciados com o uso do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. O processo inclui as seguintes etapas:  
  
1.  Selecionar uma faceta de Gerenciamento Baseado em Políticas que contenha as propriedades a serem configuradas.  
  
2.  Definir uma condição que especifique o estado de uma faceta de gerenciamento.  
  
3.  Definir uma política que contenha uma condição, as condições adicionas que filtram os conjuntos de destino e o modo de avaliação.  
  
4.  Verificar se uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em conformidade com a política.  
  
 Para as políticas com falha, o Pesquisador de Objetos indica um aviso de integridade crítica como um ícone vermelho ao lado do destino e dos nós superiores na árvore do Pesquisador de Objetos.  
  
> [!NOTE]  
>  Quando o sistema computar o objeto definido para uma política, por padrão os objetos do sistema serão excluídos.  Por exemplo, se o conjunto de objetos da política referenciar todas as tabelas, a política não se aplicará a tabelas do sistema. Se os usuários desejarem avaliar uma política em relação a objetos do sistema, eles poderão explicitamente adicionar objetos do sistema ao conjunto de objetos. Entretanto, embora todas as políticas tenham suporte para o modo de avaliação **verificação de agenda** , por questões de desempenho, nem todas as políticas com conjuntos de objetos arbitrários têm suporte para o modo de avaliação **verificação de alterações** . Para obter mais informações, consulte [http://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](http://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)  
  
## <a name="policy-based-management-concepts"></a>Conceitos do Gerenciamento Baseado em Políticas  
 O Gerenciamento Baseado em Políticas tem três componentes:  
  
-   Gerenciamento de política  
  
     Os administradores de políticas criam políticas.  
  
-   Administração explícita  
  
     Os administradores selecionam um ou mais destinos gerenciados e verificam explicitamente se eles estão de acordo com uma política específica, ou explicitamente fazem com que os destinos estejam de acordo com uma política.  
  
-   Modos de avaliação  
  
     Há quatro modos de avaliação, três dos quais podem ser automatizados:  
  
    -   **Sob demanda**. Este modo avalia a política quando especificado diretamente pelo usuário.  
  
    -   **Ao alterar: impedir**. Esse modo automatizado usa gatilhos DDL para impedir violações de política.  
  
        > [!IMPORTANT]  
        >  Se a opção de configuração do servidor gatilhos aninhados for desabilitada, **Ao alterar: impedir** não funcionará corretamente. O Gerenciamento Baseado em Políticas necessita de gatilhos DDL para detectar e reverter operações de DDL que não estejam em conformidade com políticas que usam este modo de avaliação. Remover os gatilhos DDL do Gerenciamento Baseado em Políticas ou desabilitar os gatilhos aninhados fará com que este modo de avaliação falhe ou execute de forma inesperada.  
  
    -   **Ao alterar: log apenas**. Este modo automatizado usa a notificação de eventos para avaliar uma política quando uma alteração relevante é feita.  
  
    -   **Ao agendar**. Este modo automatizado usa um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para avaliar periodicamente uma política.  
  
     Quando as políticas automatizadas não estão habilitadas, o Gerenciamento Baseado em Políticas não afetará o desempenho do sistema.  
  
## <a name="policy-based-management-terms"></a>Termos do Gerenciamento Baseado em Políticas  
 Destino gerenciado pelo Gerenciamento Baseado em Políticas  
 As entidades gerenciadas pelo Gerenciamento Baseado em Políticas, como uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], um banco de dados, uma tabela ou um índice. Todos os destinos em uma instância de servidor formam uma hierarquia de destino. Um conjunto de destino é aquele resultante da aplicação de um conjunto de filtros de destino à hierarquia de destino. Por exemplo, todas as tabelas do banco de dados de propriedade do esquema HumanResources.  
  
 Faceta do Gerenciamento Baseado em Políticas  
 Um conjunto de propriedades lógicas que modelam o comportamento ou as características de certos tipos de destinos gerenciados. O número e as características das propriedades são incorporados à faceta e só podem ser adicionados ou removidos pelo criador da faceta. Um tipo de destino pode implementar uma ou mais facetas de gerenciamento, e uma faceta de gerenciamento pode ser implementada por um ou mais tipos de destino. Algumas propriedades de uma faceta só podem ser aplicadas a uma versão específica.  
  
 Condição de Gerenciamento Baseado em Políticas  
 Uma expressão booliana que especifica um conjunto de estados permitidos de um destino gerenciado pelo Gerenciamento Baseado em Políticas em relação a uma faceta de gerenciamento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta observar agrupamentos ao avaliar uma condição. Quando os agrupamentos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não correspondem exatamente a agrupamentos do Windows, teste sua condição para determinar como o algoritmo resolve conflitos.  
  
 Política de Gerenciamento Baseado em Políticas  
 Uma condição do Gerenciamento Baseado em Políticas e o comportamento esperado, como, por exemplo, modo de avaliação, filtros de destino e agenda. Uma política só pode conter uma condição. As políticas podem ser habilitadas ou desabilitadas. As políticas são armazenadas no banco de dados msdb.  
  
 Categoria de política do Gerenciamento Baseado em Políticas  
 Uma categoria definida pelo usuário para ajudar a gerenciar políticas. Os usuários podem classificar as políticas em categorias diferentes. Uma política pertence a somente uma categoria. Categorias de políticas se aplicam a bancos de dados e servidores. No nível de banco de dados, as seguintes condições se aplicam:  
  
-   Os proprietários de banco de dados podem assinar um conjunto de categorias de política para um banco de dados.  
  
-   Somente as políticas das categorias assinadas podem governar um banco de dados.  
  
-   Todos os bancos de dados assinam implicitamente a categoria de política padrão.  
  
 No nível de servidor, é possível aplicar categorias de políticas a todos os bancos de dados.  
  
 Política efetiva  
 As políticas efetivas de um destino são aquelas que governam esse destino. Uma política só será efetiva em relação a um destino se todas as seguintes condições forem satisfeitas:  
  
-   A política está habilitada.  
  
-   O destino pertence ao conjunto de destino da política.  
  
-   O destino ou um dos destinos ancestrais assina o grupo de políticas que contém essa política.  
  
## <a name="policy-based-management-tasks"></a>Tarefas de Gerenciamento Baseado em Políticas  
 O Gerenciamento Baseado em Políticas é um sistema baseado em política para gerenciar uma ou mais instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use o Gerenciamento Baseado em Políticas para criar condições que contêm expressões de condição. Em seguida, crie políticas que se aplicam as condições a objetos de destino de banco de dados.  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como as políticas do Gerenciamento Baseado em Políticas são armazenadas.|Armazenamento do Gerenciamento Baseado em Políticas|  
|Descreve como configurar alertas para notificar os administradores de políticas sobre falhas.|[Configurar alertas para notificar os administradores sobre falhas de políticas](configure-alerts-to-notify-policy-administrators-of-policy-failures.md)|  
|Descreve como criar, exibir, modificar e excluir uma condição de Gerenciamento Baseado em Políticas.|[Criar uma nova condição de gerenciamento baseado em políticas](create-a-new-policy-based-management-condition.md)<br /><br /> [Excluir uma condição de gerenciamento baseado em políticas](delete-a-policy-based-management-condition.md)<br /><br /> [Exibir ou modificar as propriedades de uma condição de gerenciamento baseado em políticas](view-or-modify-the-properties-of-a-policy-based-management-condition.md)|  
|Descreve como criar, exibir, modificar e excluir uma política do Gerenciamento Baseado em Políticas.|[Criar uma política do gerenciamento baseado em políticas](create-a-policy-based-management-policy.md)<br /><br /> [Excluir uma política do gerenciamento baseado em políticas](delete-a-policy-based-management-policy.md)<br /><br /> [Exibir ou modificar as propriedades de uma política de gerenciamento baseado em políticas](view-or-modify-the-properties-of-a-policy-based-management-policy.md)|  
|Descreve como exportar e importar uma política do Gerenciamento Baseado em Políticas.|[Exportar uma política do gerenciamento baseado em políticas](export-a-policy-based-management-policy.md)<br /><br /> [Importar uma política de gerenciamento baseado em políticas](import-a-policy-based-management-policy.md)|  
|Descreve como verificar se uma instância de servidor, banco de dados, objeto de servidor ou objeto de banco de dados obedece a uma política.|[Avaliar uma política do gerenciamento baseado em políticas de um objeto](evaluate-a-policy-based-management-policy-from-an-object.md)<br /><br /> [Avaliar uma política do gerenciamento baseado em políticas dessa política](evaluate-a-policy-based-management-policy-from-that-policy.md)<br /><br /> [Avaliar uma política do gerenciamento baseado em políticas em um agendamento](evaluate-a-policy-based-management-policy-on-a-schedule.md)|  
|Descreve como exibir e copiar um estado de faceta de Gerenciamento Baseado em Políticas em um arquivo.|[Trabalhando com facetas do gerenciamento baseado em políticas](working-with-policy-based-management-facets.md)|  
|Fornece um conjunto de arquivos de políticas que você pode importar como políticas de práticas recomendadas e descreve como avaliar essas políticas em relação a um conjunto de destino que inclui instâncias, objetos de instância, bancos de dados ou objetos de bancos de dados.|[Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](monitor-and-enforce-best-practices-by-using-policy-based-management.md)|  
|Fornece os tópicos da Ajuda F1 para o nó **PolicyManagement** do Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|[Nó de gerenciamento de política &#40;Pesquisador de objetos&#41;](../../ssms/object/object-explorer.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/policy-based-management-views-transact-sql)  
  
  
