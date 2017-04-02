---
title: "Visualizador de Conflitos de Replica&#231;&#227;o da Microsoft (replica&#231;&#227;o de mesclagem) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.replconflictviewer.cvmerge.f1"
ms.assetid: bfef5e21-ac04-4bc5-a55e-595421e34923
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 24
---
# Visualizador de Conflitos de Replica&#231;&#227;o da Microsoft (replica&#231;&#227;o de mesclagem)
  O Visualizador de Conflitos de Replicação permite exibir qualquer conflito ocorrido durante a sincronização de replicação. Os conflitos ocorrem quando os mesmos dados são modificados em dois servidores separados, por exemplo, no Publicador e no Assinante, ou em dois Assinantes diferentes. A replicação resolve conflitos automaticamente usando o resolvedor de conflitos que você selecionou quando o artigo foi criado. No entanto, o Visualizador de Conflitos de Replicação permite escolher uma resolução diferente para o conflito quando necessário. Podem ocorrer os seguintes conflitos:  
  
-   Conflitos de atualização. Conflitos de atualização ocorrem quando os mesmos dados são alterados em dois locais. Uma alteração vence e a outra perde. Você tem a opção de manter os dados existentes (os dados vencedores), substituir os dados existentes pelos dados de conflito (os dados perdedores), ou mesclar os dados perdedores e vencedores e atualizar os dados existentes.  
  
-   Conflitos de inserção. Conflitos de inserção ocorrem quando uma linha é inserida em um local e viola alguma regra de consistência de dados ao ser mesclada com alterações em outros locais. Você tem a opção de manter os dados existentes (os dados vencedores), substituir os dados existentes pelos dados de conflito (os dados perdedores), ou mesclar os dados perdedores e vencedores e atualizar os dados existentes.  
  
-   Conflitos de exclusão. Esses conflitos ocorrem quando a mesma linha é excluída em um local e alterada em outro.  
  
 Quando conflitos são resolvidos durante a sincronização, os dados da linha perdedora são gravados em uma tabela de conflitos. Quer você aceite a resolução original ou escolha uma resolução diferente para o conflito, a linha de conflito registrada será excluída da tabela de conflitos. Você deve revisar os conflitos periodicamente para ajudar reduzir o tamanho das tabelas de controle de conflito.  
  
> [!NOTE]  
>  Não são exibidos conflitos que envolvem registros lógicos no Visualizador de Conflitos. Para exibir informações sobre esses conflitos, use procedimentos armazenados de replicação. Para obter mais informações, consulte [Exibir informações de conflito para publicações de mesclagem e 40; Programação Transact-SQL de replicação e 41;](../../relational-databases/replication/view conflict information for merge publications.md).  
  
## Opções  
 O Visualizador de Conflitos de Replicação é dividido em duas seções. A seção superior da caixa de diálogo mostra a lista de conflitos para a tabela selecionada. Quando você clica em um item na lista de conflitos, os detalhes do conflito são exibidos na seção inferior da caixa de diálogo.  
  
 Informações descrevendo o motivo do conflito (por exemplo, a mesma linha foi atualizada no Publicador e no Assinante) são exibidas na seção inferior da caixa de diálogo. Os dados de conflito na seção inferior são exibidos em duas colunas correspondentes (**vencedora do conflito** e **perdedor de conflito**). Se o conflito estiver entre os dados atualizados e excluídos, talvez não haja dados a serem exibidos no lado excluído do conflito. Nesse caso, o Visualizador de Conflitos de Replicação exibe uma mensagem em uma das colunas, indicando que a linha foi excluída em um local e atualizada em outro. Também indica a resolução sugerida.  
  
 Dados que não podem ser editados no Visualizador de conflitos de replicação (por exemplo, **rowguid** dados) é exibido somente leitura com a caixa sombreada.  
  
 **Banco de Dados**  
 Escolha um banco de dados que inclua publicações com conflitos.  
  
 **Publicação**  
 Escolha uma publicação que inclua tabelas com conflitos.  
  
 **Table**  
 Escolha uma tabela que inclua conflitos.  
  
 **Definir Filtro**  
 Clique para abrir o **definir filtros** caixa de diálogo.  
  
 **Aplicar ou Remover Filtro**  
 Clique para aplicar ou remover um filtro que foi definido no **definir filtros** caixa de diálogo.  
  
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
  
 **Exibir informações da coluna** (**...**)  
 Clique para exibir informações de coluna: **nome de tabela**, **nome de coluna**, **tipo de dados**, e **o valor da coluna**. **O valor da coluna** é editável, a menos que o valor é exibido como somente leitura.  
  
 **Enviar Vencedor**  
 Clique para manter a linha que o resolvedor de conflitos determinou como vencedora. O valor de qualquer coluna que não é exibido como somente leitura pode ser alterado antes de clicar nesse botão.  
  
 **Enviar Perdedor**  
 Clique para aceitar a linha que o resolvedor de conflitos determinou como perdedora. O valor de qualquer coluna que não é exibido como somente leitura pode ser alterado antes de clicar nesse botão.  
  
 **Registrar em log os detalhes do conflito**  
 Marque essa caixa para registrar em log os detalhes do conflito em um arquivo. Para especificar um local para o arquivo, aponte para o **exibição** menu e clique em **opções**. Insira um valor ou clique no botão Procurar (**...**) e navegue até o arquivo apropriado. Clique em **OK** para sair da caixa de diálogo **Opções** .  
  
## Consulte também  
 [Exibir e resolver conflitos de dados para publicações de mesclagem e 40; SQL Server Management Studio e 41;](../../relational-databases/replication/view and resolve data conflicts for merge publications.md)   
 [Detecção e resolução de conflito de replicação de mesclagem avançada ](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  