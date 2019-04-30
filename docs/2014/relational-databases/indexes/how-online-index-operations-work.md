---
title: Como funcionam as operações de índice online | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- online index operations
- source indexes [SQL Server]
- preexisting indexes [SQL Server]
- target indexes [SQL Server]
- temporary mapping index [SQL Server]
- index temporary mappings [SQL Server]
ms.assetid: eef0c9d1-790d-46e4-a758-d0bf6742e6ae
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 102c3d72d811627074da570ee74902e51a4b86dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63162167"
---
# <a name="how-online-index-operations-work"></a>Como funcionam as operações de índice online
  Esse tópico define as estruturas que existem durante uma operação de índice online e mostra as atividades associadas a elas.  
  
## <a name="online-index-structures"></a>Estruturas de índice online  
 Para permitir atividade de usuário simultânea durante uma operação DDL (linguagem de definição de dados) de índice, as seguintes estruturas são usadas durante a operação de índice online: índices de origem e preexistentes, destino e, para recompilar um heap ou remover um índice clusterizado online, um índice de mapeamento temporário.  
  
-   **Índices de origem e preexistentes**  
  
     A origem é a tabela original ou os dados do índice clusterizado. Índices preexistentes são quaisquer índices não clusterizados associados à estrutura de origem. Por exemplo, se a operação de índice online estiver recompilando um índice clusterizado que tenha quatro índices não clusterizados associados, a origem será o índice clusterizado existente, e os índices preexistentes serão os índices não clusterizados.  
  
     Os índices preexistentes estão disponíveis a usuários simultâneos para operações de seleção, inserção, atualização e exclusão. Isso inclui inserções em massa (aceitas mas não recomendadas) e atualizações implícitas por gatilhos e restrições de integridade referenciais. Todos os índices preexistentes estão disponíveis para consultas e pesquisas. Isso significa eles podem ser selecionados pelo otimizador de consulta e, se necessário, especificados pelas dicas de índice.  
  
-   **Target (destino)**  
  
     O destino (ou destinos) é o novo índice (ou heap) ou um conjunto de novos índices sendo criados ou recompilados. As operações de inserção, atualização e exclusão do destino são aplicadas pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] no destino durante a operação de índice. Por exemplo, se a operação de índice online estiver recompilando um índice online, o destino será o índice clusterizado recompilado; o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não recompila índices não clusterizados quando um índice clusterizado é recompilado.  
  
     O índice de destino não é pesquisado enquanto as instruções SELECT são processadas, até que a operação de índice esteja confirmada. Internamente, o índice é marcado como somente leitura.  
  
-   **Índice de mapeamento temporário**  
  
     As operações de índice online que criam, removem ou recompilam um índice clusterizado também requerem um índice de mapeamento temporário. Esse índice temporário é usado por transações simultâneas para determinar quais registros devem ser excluídos dos novos índices sendo compilados quando as linhas na tabela subjacente são atualizadas ou excluídas. Esse índice não clusterizado é criado na mesma etapa do novo índice clusterizado (ou heap) e não requer uma operação de classificação separada. As transações simultâneas também mantêm o índice de mapeamento temporário em todas as operações de inserção, atualização e exclusão.  
  
## <a name="online-index-activities"></a>Atividades do índice online  
 Durante uma operação de índice online simples, como por exemplo a criação de um índice clusterizado em uma tabela não indexada (heap), a origem e o destino passam por essas três fases: preparação, compilação e finalização.  
  
 A ilustração a seguir mostra o processo para criar um índice clusterizado online inicial. O objeto de origem (o heap) não tem outros índices. As atividades de estrutura de origem e destino são mostradas para cada fase; as operações de seleção, inserção, atualização e exclusão de usuários simultâneos também são mostradas. As fases de preparação, compilação e finalização são indicadas junto com os modos de bloqueio usados em cada fase.  
  
 ![Atividades executadas durante a operação de índice online](../../database-engine/media/online-index.gif "Atividades executadas durante a operação de índice online")  
  
## <a name="source-structure-activities"></a>Atividades da estrutura de origem  
 A tabela a seguir lista as atividades envolvendo as estruturas de origem durante cada fase da operação de índice e a estratégia de bloqueio correspondente.  
  
|Fase|Atividade de origem|Bloqueios de origem|  
|-----------|---------------------|------------------|  
|Preparação<br /><br /> Fase muito curta|Preparação dos metadados do sistema para criar uma nova estrutura de índice vazia.<br /><br /> Um instantâneo da tabela é definido. Ou seja, o controle de versão de linha é usado para fornecer uma consistência de leitura em nível de transação.<br /><br /> As operações de usuário simultâneas de gravação na origem são bloqueadas por um período muito curto.<br /><br /> Operações DLL não simultâneas são permitidas, exceto na criação de múltiplos índices não clusterizados.|S (Shared) na tabela *<br /><br /> IS (Intent Shared)<br /><br /> INDEX_BUILD_INTERNAL_RESOURCE\*\*|  
|Compilação<br /><br /> Fase principal|Os dados são digitalizados, classificados, mesclados e inseridos na origem em operações de carregamento em massa.<br /><br /> As operações de usuário simultâneas de exclusão, atualização, inserção e seleção são aplicadas aos índices preexistentes e a quaisquer outros novos índices sendo compilados.|IS<br /><br /> INDEX_BUILD_INTERNAL_RESOURCE**|  
|Final<br /><br /> Fase muito curta|Todas as transações atualizadas não confirmadas devem ser concluídas antes do início desta fase. Dependendo do bloqueio adquirido, todas as novas transações de usuário de leitura ou gravação devem ser bloqueadas por um período muito curto até que essa fase seja completada.<br /><br /> Os metadados do sistema estão atualizados para substituir a origem pelo destino.<br /><br /> Se necessário, a origem será removida. Por exemplo, depois de recompilar e remover um índice clusterizado.|INDEX_BUILD_INTERNAL_RESOURCE**<br /><br /> S na tabela se estiver criando um índice não clusterizado.\*<br /><br /> SCH-M (Schema Modification) se qualquer estrutura de origem (índice ou tabela) for removida.\*|  
  
 \* A operação de índice aguardará a conclusão de transações de atualização não confirmadas antes de adquirir o bloqueio S ou SCH-M na tabela.  
  
 ** O bloqueio de recurso INDEX_BUILD_INTERNAL_RESOURCE evita a execução de operações DDL (linguagem de definição de dados) simultâneas nas estruturas de origem e preexistentes enquanto a operação de índice está em andamento. Por exemplo, esse bloqueio evita a recompilação simultânea de dois índices na mesma tabela. Embora esse bloqueio de recurso esteja associado ao bloqueio Sch-M, ele não evita as instruções de manipulação de dados.  
  
 A tabela anterior mostra um único bloqueio Shared (S) adquirido durante a fase de compilação de uma operação de índice online que envolve um único índice. Quando índices clusterizados e não clusterizados são compilados ou recompilados em uma única operação de índice online (por exemplo, durante a criação de índice clusterizado inicial em uma tabela que contém um ou mais índices não clusterizados), dois bloqueios S de curto prazo são adquiridos durante a fase de compilação, seguidos de bloqueios IS (Tentativa Compartilhada) de longo prazo. Um bloqueio S é adquirido primeiramente para a criação de índice clusterizado e, quando a criação do índice clusterizado é concluída, um bloqueio S de curta duração é adquirido para a criação dos índices não clusterizados. Depois que os índices não clusterizados são criados, ocorre o downgrade do bloqueio S para um bloqueio IS até a fase final da operação de índice online.  
  
### <a name="target-structure-activities"></a>Atividades da estrutura de destino  
 A tabela a seguir lista as atividades que envolvem as estruturas destino durante cada fase da operação de índice e a estratégia de bloqueio correspondente.  
  
|Fase|Atividade de destino|Bloqueios de destino|  
|-----------|---------------------|------------------|  
|Preparação|Um novo índice é criado e definido como somente gravação.|IS|  
|Compilação|Os dados são inseridos a partir da origem.<br /><br /> São aplicadas as modificações de usuário (inserções, atualizações, exclusões) aplicadas à origem.<br /><br /> Esta atividade é transparente ao usuário.|IS|  
|Final|Os metadados do índice são atualizados.<br /><br /> O índice é definido para o status de leitura/gravação.|P<br /><br /> ou em<br /><br /> SCH-M|  
  
 O destino não é acessado por instruções SELECT emitidas pelo usuário até que a operação de índice seja concluída.  
  
 Após a conclusão da preparação e da fase final, os planos de consulta e atualização armazenados no cache de procedimento são invalidados. As consultas subsequentes usarão o novo índice.  
  
 O tempo de vida de um cursor declarado em uma tabela que está envolvida em uma operação de índice online é limitado pelas fases de índice online. Os cursores de atualização são invalidados em cada fase. Os cursores somente leitura são invalidados somente após a fase final.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Executar operações de índice online](perform-index-operations-online.md)  
  
 [Diretrizes para operações de índice online](guidelines-for-online-index-operations.md)  
  
  
