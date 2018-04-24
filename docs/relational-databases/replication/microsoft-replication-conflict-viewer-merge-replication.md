---
title: Visualizador de Conflitos de Replicação da Microsoft (replicação de mesclagem) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.replconflictviewer.cvmerge.f1
ms.assetid: bfef5e21-ac04-4bc5-a55e-595421e34923
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8835a4aa6a8e9b58f4b984a90c755f59e343936f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="microsoft-replication-conflict-viewer-merge-replication"></a>Visualizador de Conflitos de Replicação da Microsoft (replicação de mesclagem)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O Visualizador de Conflitos de Replicação permite exibir qualquer conflito ocorrido durante a sincronização de replicação. Os conflitos ocorrem quando os mesmos dados são modificados em dois servidores separados, por exemplo, no Publicador e no Assinante, ou em dois Assinantes diferentes. A replicação resolve conflitos automaticamente usando o resolvedor de conflitos que você selecionou quando o artigo foi criado. No entanto, o Visualizador de Conflitos de Replicação permite escolher uma resolução diferente para o conflito quando necessário. Podem ocorrer os seguintes conflitos:  
  
-   Conflitos de atualização. Conflitos de atualização ocorrem quando os mesmos dados são alterados em dois locais. Uma alteração vence e a outra perde. Você tem a opção de manter os dados existentes (os dados vencedores), substituir os dados existentes pelos dados de conflito (os dados perdedores), ou mesclar os dados perdedores e vencedores e atualizar os dados existentes.  
  
-   Conflitos de inserção. Conflitos de inserção ocorrem quando uma linha é inserida em um local e viola alguma regra de consistência de dados ao ser mesclada com alterações em outros locais. Você tem a opção de manter os dados existentes (os dados vencedores), substituir os dados existentes pelos dados de conflito (os dados perdedores), ou mesclar os dados perdedores e vencedores e atualizar os dados existentes.  
  
-   Conflitos de exclusão. Esses conflitos ocorrem quando a mesma linha é excluída em um local e alterada em outro.  
  
 Quando conflitos são resolvidos durante a sincronização, os dados da linha perdedora são gravados em uma tabela de conflitos. Quer você aceite a resolução original ou escolha uma resolução diferente para o conflito, a linha de conflito registrada será excluída da tabela de conflitos. Você deve revisar os conflitos periodicamente para ajudar reduzir o tamanho das tabelas de controle de conflito.  
  
> [!NOTE]  
>  Não são exibidos conflitos que envolvem registros lógicos no Visualizador de Conflitos. Para exibir informações sobre esses conflitos, use procedimentos armazenados de replicação. Para obter mais informações, consulte [Exibir informações sobre conflitos em publicações de mesclagem &#40;Programação Transact-SQL de replicação&#41;](../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
## <a name="options"></a>Opções  
 O Visualizador de Conflitos de Replicação é dividido em duas seções. A seção superior da caixa de diálogo mostra a lista de conflitos para a tabela selecionada. Quando você clica em um item na lista de conflitos, os detalhes do conflito são exibidos na seção inferior da caixa de diálogo.  
  
 Informações descrevendo o motivo do conflito (por exemplo, a mesma linha foi atualizada no Publicador e no Assinante) são exibidas na seção inferior da caixa de diálogo. Os dados de conflito na seção inferior são exibidos em duas colunas correspondentes (**Vencedor do Conflito** e **Perdedor do Conflito**). Se o conflito estiver entre os dados atualizados e excluídos, talvez não haja dados a serem exibidos no lado excluído do conflito. Nesse caso, o Visualizador de Conflitos de Replicação exibe uma mensagem em uma das colunas, indicando que a linha foi excluída em um local e atualizada em outro. Também indica a resolução sugerida.  
  
 Dados que não podem ser editados no Visualizador de Conflitos de Replicação (por exemplo, dados **rowguid** ) serão exibidos como somente leitura com a caixa sombreada.  
  
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
 Clique para remover conflitos selecionados do visualizador e seus metadados associados das tabelas do sistema de replicação. Equivalente a clicar no botão Enviar Vencedor (sem fazer qualquer alteração nos dados) para cada conflito selecionado.  
  
 **Mostrar todas as colunas**  
 Selecione para mostrar todas as colunas da tabela.  
  
 **Mostrar as primeiras cinco colunas e outras colunas com dados conflitantes**  
 Selecione para exibir as primeiras cinco colunas e qualquer coluna com conflitos. Isso é útil quando a tabela tem um grande número de colunas, mas você quer ver apenas as mais relevantes para resolver o conflito. As primeiras cinco colunas sempre são incluídas nessa exibição, como campos que identificam uma linha, como chave primária ou campo de nomes, estão sempre entre as primeiras colunas da tabela.  
  
 **Exibir Informações da Coluna** (**.**)  
 Clique para exibir informações da coluna: **Nome da Tabela**, **Nome da Coluna**, **Tipo de Dados**e **Valor da Coluna**. **Valor da Coluna** é editável, a menos que o valor seja exibido como somente leitura.  
  
 **Enviar Vencedor**  
 Clique para manter a linha que o resolvedor de conflitos determinou como vencedora. O valor de qualquer coluna que não é exibido como somente leitura pode ser alterado antes de clicar nesse botão.  
  
 **Enviar Perdedor**  
 Clique para aceitar a linha que o resolvedor de conflitos determinou como perdedora. O valor de qualquer coluna que não é exibido como somente leitura pode ser alterado antes de clicar nesse botão.  
  
 **Registrar em log os detalhes do conflito**  
 Marque essa caixa para registrar em log os detalhes do conflito em um arquivo. Para especificar um local para o arquivo, aponte para o menu **Exibir** e clique em **Opções**. Insira um valor ou clique em (**...**) e navegue até o arquivo apropriado. Clique em **OK** para sair da caixa de diálogo **Opções** .  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e resolver conflitos de dados em publicações de mesclagem &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
