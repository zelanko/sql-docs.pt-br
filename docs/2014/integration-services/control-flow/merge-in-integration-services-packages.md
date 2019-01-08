---
title: MERGE em pacotes do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- MERGE statement [SQL Server]
ms.assetid: 7e44a5c2-e6d6-4fe2-a079-4f95ccdb147b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cffe029abd6774262e7aad12ad7aade07717bc80
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359278"
---
# <a name="merge-in-integration-services-packages"></a>MERGE em pacotes do Integration Services
  Na versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], a instrução SQL em uma tarefa Executar SQL pode conter uma instrução MERGE. A instrução MERGE permite realizar várias operações INSERT, UPDATE e DELETE em uma única instrução.  
  
 Para usar a instrução MERGE em um pacote, siga estas etapas:  
  
-   Crie uma tarefa Fluxo de Dados que carrega, transforma e salva os dados de origem em uma tabela temporária ou de preparação.  
  
-   Crie uma tarefa Executar SQL que contém a instrução MERGE.  
  
-   Conecte a tarefa Fluxo de Dados à tarefa Executar SQL e use os dados da tabela de preparação como entrada para a instrução MERGE.  
  
    > [!NOTE]  
    >  Embora uma instrução MERGE normalmente precise de uma tabela de preparação nesse caso, o desempenho da instrução MERGE, em geral, ultrapassa o desempenho da pesquisa de linha por linha executada pela transformação Pesquisa. A instrução MERGE também é útil quando o tamanho grande de uma tabela de pesquisa testa a memória disponível para a transformação Pesquisa armazenar a tabela de referência em cache.  
  
 O restante deste tópico discute alguns usos adicionais da instrução MERGE.  
  
 Para um componente de destino de exemplo que oferece suporte ao uso da instrução MERGE, consulte o exemplo da comunidade CodePlex, [Destino MERGE](https://go.microsoft.com/fwlink/?LinkId=141215).  
  
## <a name="using-merge"></a>Usando MERGE  
 Normalmente, você usa a instrução MERGE quando deseja aplicar alterações que incluem inserções, atualizações e exclusões de uma tabela para outra. Antes do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], este processo precisava de uma transformação Pesquisa e de várias transformações Comando OLE DB. A transformação Pesquisa executava uma pesquisa em linha por linha para determinar se cada linha era nova ou tinha sido alterada. Em seguida, as transformações Comando OLE DB executavam as operações INSERT, UPDATE e DELETE necessárias. A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], uma única instrução MERGE pode substituir a transformação Pesquisa e as transformações Comando OLE DB correspondentes.  
  
### <a name="merge-with-incremental-loads"></a>MERGE com cargas incrementais  
 A funcionalidade de alteração da captura dos dados que é nova no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] facilita a execução de cargas incrementais com segurança em um data warehouse. Como alternativa para o uso de transformações Comando OLE DB parametrizadas para executar as inserções e atualizações, você pode usar a instrução MERGE para combinar as duas operações.  
  
 Para obter mais informações, consulte [Aplicar as alterações ao destino](../change-data-capture/apply-the-changes-to-the-destination.md).  
  
#### <a name="merge-in-other-scenarios"></a>MERGE em outros cenários  
 Nos cenários a seguir, você pode usar a instrução MERGE fora ou dentro de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . No entanto, um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] geralmente deve carregar esses dados a partir de várias fontes heterogêneas e, em seguida, combinar e limpar os dados. Desse modo, é aconselhável usar a instrução MERGE em um pacote para que você tenha mais praticidade e seja mais fácil executar a manutenção.  
  
##### <a name="track-buying-habits"></a>Acompanhar hábitos de compra  
 A tabela FactBuyingHabits no data warehouse rastreia a última data em que um cliente comprou um determinado produto. A tabela consiste nas colunas ProductID, CustomerID e PurchaseDate. Todas as semanas, o banco de dados transacional gera uma tabela PurchaseRecords que inclui as compras feitas durante aquela semana. O objetivo é usar uma única instrução MERGE para mesclar as informações da tabela PurchaseRecords na tabela FactBuyingHabits. Para os pares produto-cliente que não existem, a instrução MERGE insere linhas novas. Para os pares produto-cliente que existem, a instrução MERGE atualiza a data de compra mais recente.  
  
###### <a name="track-price-history"></a>Acompanhar o histórico de preços  
 A tabela DimBook representa a lista de livros do inventário de um vendedor de livros e identifica o histórico de preços de cada livro. Esta tabela tem as seguintes colunas: ISBN, ProductID, Price, Shelf e IsCurrent. Esta tabela também tem uma linha para cada preço que o livro já teve. Uma dessas linhas contém o preço atual. Para indicar qual linha contém o preço atual, o valor da coluna IsCurrent para essa linha é definido como 1.  
  
 Todas as semanas, o banco de dados gera uma tabela WeeklyChanges que contém as alterações de preço da semana e os novos livros que foram adicionados durante a semana. Usando uma única instrução MERGE, você pode aplicar as alterações da tabela WeeklyChanges na tabela DimBook. A instrução MERGE insere novas linhas para os livros adicionados recentemente e atualiza a coluna IsCurrent para 0 nas linhas dos livros existentes cujo preço foi alterado. A instrução MERGE também insere novas linhas para os livros cujo preço foi alterado e, para essas novas linhas, define o valor da coluna IsCurrent como 1.  
  
### <a name="merge-a-table-with-new-data-against-the-old-table"></a>Mesclar uma tabela com dados novos em uma tabela antiga  
 O banco de dados define as propriedades de um objeto usando um "esquema aberto", ou seja, uma tabela que contém pares nome-valor para cada propriedade. A tabela Properties tem três colunas: EntityID, PropertyID e Value. Uma tabela NewProperties que é uma versão mais nova da tabela deve ser sincronizada com a tabela Properties. Para sincronizar essas duas tabelas, você pode usar uma única instrução MERGE para executar as seguintes operações:  
  
-   Exclua propriedades da tabela Properties se elas não existirem na tabela NewProperties.  
  
-   Atualize os valores das propriedades que estão na tabela Properties com os novos valores encontrados na tabela NewProperties.  
  
-   Insira novas propriedades para as propriedades que estão na tabela NewProperties, mas não são encontradas na tabela Properties.  
  
 Essa abordagem é útil em cenários que lembram cenários de replicação, onde o objetivo é manter os dados das duas tabelas em dois servidores sincronizados.  
  
### <a name="track-inventory"></a>Acompanhar o inventário  
 O banco de dados Inventory tem uma tabela ProductsInventory que tem as colunas ProductID e StockOnHand. Uma tabela Shipments com as colunas ProductID, CustomerID e Quantity rastreia o envio de produtos para os clientes. A tabela ProductInventory deve ser atualizada diariamente com base nas informações da tabela Shipments. Uma única instrução MERGE pode reduzir o inventário na tabela ProductInventory com base nas remessas feitas. Se o inventário de um produto for reduzido a 0, a instrução MERGE também poderá excluir a linha desse produto da tabela ProductInventory.  
  
  
