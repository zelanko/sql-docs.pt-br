---
title: "Visualizador de Conflitos de Replicação da Microsoft (replicação transacional) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.replconflictviewer.cvqueued.f1
ms.assetid: eec59d8e-cadb-4623-a31f-9f42ec09c97f
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 84f634a20b64b754a696692ac9b860e686f2b786
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="microsoft-replication-conflict-viewer-transactional-replication"></a>Visualizador de Conflitos de Replicação da Microsoft (replicação transacional)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O Visualizador de Conflitos de Replicação permite exibir conflitos que ocorreram durante a sincronização para uma replicação transacional ponto a ponto de uma replicação transacional com assinaturas de atualização enfileiradas. Para obter mais informações, consulte [Exibir conflitos de dados em publicações transacionais &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md).  
  
> [!NOTE]  
>  O Visualizador de Conflitos de Replicação exibe conflitos que ocorrem em replicação de mesclagem e em replicação transacional. Para replicação transacional, você pode usar o Visualizador de Conflitos de Replicação para exibir dados de conflito, mas não pode escolher uma solução diferente para o conflito.  
  
## <a name="options"></a>Opções  
 O Visualizador de Conflitos de Replicação é dividido em duas seções. A seção superior da caixa de diálogo mostra a lista de conflitos para a tabela selecionada. Quando você clica em um item na lista de conflitos, os detalhes do conflito são exibidos na seção inferior da caixa de diálogo.  
  
 Os dados de conflito na seção inferior são exibidos em duas colunas correspondentes (**Vencedor do Conflito** e **Perdedor do Conflito**). Se o conflito estiver entre os dados atualizados e excluídos, talvez não haja dados a serem exibidos no lado excluído do conflito. Nesse caso, o Visualizador de Conflitos de Replicação exibe uma mensagem em uma das colunas, indicando que a linha foi excluída em um local e atualizada em outro. Também indica a resolução sugerida.  
  
 **Backup de banco de dados**  
 Escolha um banco de dados que inclua publicações com conflitos.  
  
 **Publicação**  
 Escolha uma publicação que inclua tabelas com conflitos.  
  
 **Table**  
 Escolha uma tabela que inclua conflitos.  
  
 **Definir Filtro**  
 Clique para abrir a caixa de diálogo **Definir Filtros** .  
  
 **Aplicar ou Remover Filtro**  
 Clique para aplicar ou remover um filtro definido na caixa de diálogo **Definir Filtros** .  
  
 **Selecionar Tudo**  
 Clique para selecionar todos os conflitos listados na grade.  
  
 **Selecionar Nenhum**  
 Clique para desmarcar a seleção de todos os conflitos listados na grade.  
  
 **Remover**  
 Clique para remover conflitos selecionados do visualizador e seus metadados associados das tabelas do sistema de replicação.  
  
 **Mostrar todas as colunas**  
 Selecione para mostrar todas as colunas da tabela.  
  
 **Mostrar as primeiras cinco colunas e outras colunas com dados conflitantes**  
 Selecione para exibir as primeiras cinco colunas e qualquer coluna com conflitos. Isso é útil quando a tabela tem um grande número de colunas, mas você quer ver apenas as mais relevantes para resolver o conflito. As primeiras cinco colunas sempre são incluídas nessa exibição, como campos que identificam uma linha, como chave primária ou campo de nomes, estão sempre entre as primeiras colunas da tabela.  
  
 **Exibir Informações da Coluna** (**.**)  
 Clique para exibir informações da coluna: **Nome da Tabela**, **Nome da Coluna**, **Tipo de Dados**e **Valor da Coluna**.  
  
 **Registrar em log os detalhes do conflito**  
 Marque essa caixa para registrar em log os detalhes do conflito em um arquivo. Para especificar um local para o arquivo, aponte para o menu **Exibir** e clique em **Opções**. Insira um valor ou clique em (**...**) e navegue até o arquivo apropriado. Clique em **OK** para sair da caixa de diálogo **Opções** .  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção de conflitos na replicação ponto a ponto](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [Exibir conflitos de dados em publicações transacionais &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
  
