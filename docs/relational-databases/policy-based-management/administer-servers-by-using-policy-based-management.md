---
title: Administrar servidores com Gerenciamento Baseado em Políticas | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c62c2372b0a61d0a09a0e15998f2340b995fc919
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109931"
---
# <a name="administer-servers-by-using-policy-based-management"></a>Administrar servidores com Gerenciamento Baseado em Políticas
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
   O Gerenciamento Baseado em Políticas é um sistema baseado em política para gerenciar uma ou mais instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Usado para criar condições que contêm expressões de condição. Em seguida, crie políticas que se aplicam as condições a objetos de destino de banco de dados.  

Por exemplo, como o administrador de banco de dados, é recomendável garantir que alguns servidores não tenham o Database Mail habilitado, para que você possa criar uma condição e uma política que define essa opção do servidor. 
   
 > **IMPORTANTE:** As políticas podem afetar o funcionamento de alguns recursos. Por exemplo, a captura de dados de alterações e a replicação transacional usam uma tabela systranschemas que não possui um índice. Se você habilitar uma política em que todas as tabelas devam ter um índice, a imposição de conformidade da política causará falha nesses recursos.  
  
 Use o SQL Server Management Studio para criar e gerenciar políticas, para:
  
1.  Selecionar uma faceta de Gerenciamento Baseado em Políticas que contenha as propriedades a serem configuradas.  
  
2.  Definir uma condição que especifique o estado de uma faceta de gerenciamento.  
  
3.  Definir uma política que contenha uma condição, as condições adicionas que filtram os conjuntos de destino e o modo de avaliação.  
  
4.  Verificar se uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em conformidade com a política.  
  
 Para as políticas com falha, o Pesquisador de Objetos indica um aviso de integridade crítica como um ícone vermelho ao lado do destino e dos nós superiores na árvore do Pesquisador de Objetos.  
  
> **OBSERVAÇÃO:** Quando o sistema computar o objeto definido para uma política, por padrão os objetos do sistema serão excluídos.  Por exemplo, se o conjunto de objetos da política referenciar todas as tabelas, a política não se aplicará a tabelas do sistema. Se os usuários desejarem avaliar uma política em relação a objetos do sistema, eles poderão explicitamente adicionar objetos do sistema ao conjunto de objetos. Entretanto, embora todas as políticas tenham suporte para o modo de avaliação **verificação de agenda** , por questões de desempenho, nem todas as políticas com conjuntos de objetos arbitrários têm suporte para o modo de avaliação **verificação de alterações** . Para obter mais informações, consulte [https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx)  
  
## <a name="three-policy-based-management-components"></a>Três componentes do Gerenciamento Baseado em Políticas  
 O Gerenciamento Baseado em Políticas tem três componentes:  
  
-   Gerenciamento de política. Os administradores de políticas criam políticas.  
  
-   Administração explícita. Os administradores selecionam um ou mais destinos gerenciados e verificam explicitamente se eles estão de acordo com uma política específica, ou explicitamente fazem com que os destinos estejam de acordo com uma política.  
  
-   Modos de avaliação. Há quatro modos de avaliação, três dos quais podem ser automatizados:  
  
    -   **Sob demanda**. Este modo avalia a política quando especificado diretamente pelo usuário.  
  
    -   **Ao alterar: impedir**. Esse modo automatizado usa gatilhos DDL para impedir violações de política.  
  
        > **IMPORTANTE:** Se a opção de configuração do servidor gatilhos aninhados for desabilitada, **Ao alterar: impedir** não funcionará corretamente. O Gerenciamento Baseado em Políticas necessita de gatilhos DDL para detectar e reverter operações de DDL que não estejam em conformidade com políticas que usam este modo de avaliação. Remover os gatilhos DDL do Gerenciamento Baseado em Políticas ou desabilitar os gatilhos aninhados fará com que este modo de avaliação falhe ou execute de forma inesperada.  
  
    -   **Ao alterar: log apenas**. Este modo automatizado usa a notificação de eventos para avaliar uma política quando uma alteração relevante é feita.  
  
    -   **Ao agendar**. Este modo automatizado usa um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para avaliar periodicamente uma política.  
  
     Quando as políticas automatizadas não estão habilitadas, o Gerenciamento Baseado em Políticas não afetará o desempenho do sistema.  
  
## <a name="terms"></a>Termos  
 **Destino gerenciado pelo Gerenciamento Baseado em Políticas** Entidades que são gerenciadas pelo Gerenciamento Baseado em Políticas, como uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], um banco de dados, uma tabela ou um índice. Todos os destinos em uma instância de servidor formam uma hierarquia de destino. Um conjunto de destino é aquele resultante da aplicação de um conjunto de filtros de destino à hierarquia de destino. Por exemplo, todas as tabelas do banco de dados de propriedade do esquema HumanResources.  
  
 **Faceta do Gerenciamento Baseado em Políticas** Um conjunto de propriedades lógicas que modelam o comportamento ou as características de alguns tipos de destinos gerenciados. O número e as características das propriedades são incorporados à faceta e só podem ser adicionados ou removidos pelo criador da faceta. Um tipo de destino pode implementar uma ou mais facetas de gerenciamento, e uma faceta de gerenciamento pode ser implementada por um ou mais tipos de destino. Algumas propriedades de uma faceta só podem ser aplicadas a uma versão específica.  
  
 **Condição de Gerenciamento Baseado em Políticas**  
 Uma expressão booliana que especifica um conjunto de estados permitidos de um destino gerenciado pelo Gerenciamento Baseado em Políticas em relação a uma faceta de gerenciamento. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta observar ordenações ao avaliar uma condição. Quando as ordenações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não correspondem exatamente às ordenações do Windows, teste sua condição para determinar como o algoritmo resolve conflitos.  
  
 **Política de Gerenciamento Baseado em Políticas**  
 Uma condição do Gerenciamento Baseado em Políticas e o comportamento esperado, como, por exemplo, modo de avaliação, filtros de destino e agenda. Uma política só pode conter uma condição. As políticas podem ser habilitadas ou desabilitadas. As políticas são armazenadas no banco de dados msdb.  
  
 **Categoria de política do Gerenciamento Baseado em Políticas**  
 Uma categoria definida pelo usuário para ajudar a gerenciar políticas. Os usuários podem classificar as políticas em categorias diferentes. Uma política pertence a somente uma categoria. Categorias de políticas se aplicam a bancos de dados e servidores. No nível de banco de dados, as seguintes condições se aplicam:  
  
-   Os proprietários de banco de dados podem assinar um conjunto de categorias de política para um banco de dados.  
  
-   Somente as políticas das categorias assinadas podem governar um banco de dados.  
  
-   Todos os bancos de dados assinam implicitamente a categoria de política padrão.  
  
 No nível de servidor, é possível aplicar categorias de políticas a todos os bancos de dados.  
  
 **Política efetiva**  
 As políticas efetivas de um destino são aquelas que governam esse destino. Uma política só será efetiva em relação a um destino se todas as seguintes condições forem satisfeitas:  
  
-   A política está habilitada.  
  
-   O destino pertence ao conjunto de destino da política.  
  
-   O destino ou um dos destinos ancestrais assina o grupo de políticas que contém essa política.  
  
## <a name="links-to-specific-tasks"></a>Links para tarefas específicas 

 - [Armazenar as políticas de Gerenciamento Baseado em Políticas.](policy-based-management-storage.md)|  
 - [Configurar alertas para notificar os administradores de políticas sobre falhas](../../relational-databases/policy-based-management/configure-alerts-to-notify-policy-administrators-of-policy-failures.md)  
 - [Criar uma nova condição de Gerenciamento baseado em Políticas](../../relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) 
 - [Excluir uma condição de Gerenciamento baseado em Políticas](../../relational-databases/policy-based-management/delete-a-policy-based-management-condition.md)
 - [Exibir ou modificar as propriedades de uma condição de gerenciamento baseado em políticas](../../relational-databases/policy-based-management/view-or-modify-the-properties-of-a-policy-based-management-condition.md)|  
 - [Exportar uma política do Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/export-a-policy-based-management-policy.md)
 - [Importar política de Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md)|  
 - [Avaliar uma política do Gerenciamento Baseado em Políticas de um objeto](../../relational-databases/policy-based-management/evaluate-a-policy-based-management-policy-from-an-object.md)
 - [Trabalhar com facetas do Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)|  
 - [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)


## <a name="see-also"></a>Confira também  
 
 - [Tutorial: Criar e aplicar uma política desativada por padrão](lesson-1-create-and-apply-an-off-by-default-policy.md)
 - [Tutorial: Criar e aplicar uma política de padrões de nomenclatura](lesson-2-create-and-apply-a-naming-standards-policy.md)
 - [Exibições de Gerenciamento Baseado em Políticas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
 

 
  
  
