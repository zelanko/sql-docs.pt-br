---
title: Agrupar alterações a linhas relacionadas com registros lógicos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ad76799c-4486-4b98-9705-005433041321
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 423cbb00f8c28cc1abca309c5a2d518da4511f1a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175839"
---
# <a name="group-changes-to-related-rows-with-logical-records"></a>Agrupar alterações a linhas relacionadas com registros lógicos
  
> [!NOTE]
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]

 Por padrão, os dados de processos de replicação de mesclagem são alterados em uma base de linha por linha. Em muitas circunstâncias isto é apropriado, mas para alguns aplicativos, é essencial que as linhas relacionadas sejam processadas como uma unidade. O recurso de registro lógico de replicação de mesclagem permite que você defina uma relação entre linhas relacionadas em diferentes tabelas para que as linhas sejam processadas como uma unidade.

> [!NOTE]
>  O recurso de registros lógicos pode ser usado só ou junto com filtros de junção. Para obter mais informações sobre filtros de junção, consulte [Join Filters](join-filters.md). Para usar registros lógicos, o nível de compatibilidade da publicação deve ser pelo menos 90RTM.

 Considere estas três tabelas relacionadas:

 ![Registro lógico de três tabelas, somente com nomes de coluna](../media/logical-records-01.gif "Registro lógico de três tabelas, somente com nomes de coluna")

 A tabela **Customers** é a tabela pai nesta relação e tem uma coluna de chave primária **CustID**. A tabela **Orders** tem uma coluna de chave primária **OrderID**, com uma restrição de chave estrangeira na coluna **CustID** que faz referência à coluna **CustID** na tabela **Customers** . De forma semelhante, a tabela **OrderItems** tem uma coluna de chave primária **OrderItemID**, com uma restrição de chave estrangeira na coluna **OrderID** que faz referência à coluna **OrderID** na tabela **Orders** .

 Neste exemplo, um registro lógico consiste de todas as linhas na tabela **Orders** que são relacionadas a um valor **CustID** único e todas as linhas na tabela **OrderItems** são relacionadas a aquelas linhas na tabela **Orders** . Este diagrama exibe todas as linhas nas três tabelas que estão no registro lógico para Customer2:

 ![Registro lógico de três tabelas com valores](../media/logical-records-02.gif "Registro lógico de três tabelas com valores")

 Definir uma relação de registro lógico entre artigos, consulte [Definir uma relação de registro lógico entre artigos da tabela de mesclagem](../publish/define-a-logical-record-relationship-between-merge-table-articles.md).

## <a name="benefits-of-logical-records"></a>Benefícios de registros lógicos
 O recurso de registros lógicos tem dois benefícios primários:

-   Aplicação de alterações de dados como uma unidade.

-   A detecção e resolução de conflitos simultaneamente em várias linhas de várias tabelas.

### <a name="the-application-of-changes-as-a-unit"></a>A aplicação de alterações como uma unidade
 Se o processamento de mesclagem for interrompido, como no caso de uma conexão descartada, o conjunto parcialmente completado de alterações replicadas relacionadas será revertido se forem usados registros lógicos. Por exemplo, considere o caso onde um Assinante adiciona um novo pedido com **OrderID** = 6 e duas novas linhas na tabela **OrderItems** com **OrderItemID** = 10 e **OrderItemID** = 11 para **OrderID** = 6.

 ![Registro lógico de três tabelas com valores](../media/logical-records-04.gif "Registro lógico de três tabelas com valores")

 Se o processo de replicação for interrompido depois da linha **Pedidos** , para **OrderID** = 6 está concluído, mas, antes que os **OrderItems** 10 e 11 sejam concluídos e os registros lógicos não sejam usados, o valor de **OrderTotal** para **OrderID** = 6 não será consistente com a soma dos valores **OrderAmount** das linhas **OrderItems** . Se forem usados registros lógicos, a linha **Orders** para **OrderID** = 6 não será confirmada até que as alterações **OrderItems** sejam replicadas.

 Em um cenário diferente, se forem usados registros lógicos e alguém estiver consultando tabelas quando o processo de mesclagem estiver aplicando alterações, o usuário não verá alterações replicadas parcialmente até que todas elas sejam concluídas. Por exemplo, se o processo de replicação tiver carregado a linha de Pedidos para **OrderID** = 6, mas um usuário consultar as tabelas antes que o processo de replicação tenha replicado as linhas de **OrderItems** , o valor de **OrderTotal** não será o mesmo da soma dos valores de **OrderAmount** . Se forem usados registros lógicos, a linha de **Pedidos** não será visível ate que as linhas de **OrderItems** sejam concluídas e a transação seja confirmada como uma unidade.

### <a name="the-application-of-conflict-handling-to-more-than-one-table"></a>A aplicação de manipulação de conflito para mais do que uma tabela
 Considere o caso e quem dois Assinantes têm os dados acima definidos:

-   Um usuário no primeiro Assinante altera o **OrderAmount** do **OrderItemID** 5 de 100 para 150 e o **OrderTotal** do **OrderID** 3 de 200 para 250.

-   Um usuário no segundo Assinante altera o **OrderAmount** do **OrderItemID** 6 de 25 para 125 e o **OrderTotal** do **OrderID** 3 de 200 para 300.

 Se essas alterações forem replicadas sem usar registros lógicos, os valores diferentes de **OrderTotal** resultarão em um conflito e apenas um deles será replicado. Mas as alterações não conflitantes na tabela **OrderItems** serão replicadas sem conflito, deixando os valores finais **OrderTotal** em um estado inconsistente em relação às linhas **OrderItems** . Se forem usados registros lógicos neste cenário, a alteração de **OrderItems** associada com a alteração perdida da tabela **Orders** será revertida e o valor final de **OrderTotal** será um resumo preciso das linhas de **OrderItems** .

 Para mais informações sobre as opções relacionadas à detecção e à resolução de conflitos com registros lógicos, consulte [Detectando e resolvendo conflitos em registros lógicos](advanced-merge-replication-conflict-resolving-in-logical-record.md).

## <a name="considerations-for-using-logical-records"></a>Considerações para usar registros lógicos
 Lembre-se das seguintes considerações ao usar registros lógicos:

### <a name="general-considerations"></a>Considerações gerais

-   É recomendável que você mantenha o número de tabelas em um registro lógico o mais baixo possível; cinco tabelas ou menos é o recomendável.

-   Registros lógicos não podem fazer referência a colunas com quaisquer dos tipos de dados seguintes:

    -   `varchar(max)` e `nvarchar(max)`

    -   `varbinary(max)`

    -   `text` e `ntext`

    -   `image`

    -   `XML`

    -   `UDT`

-   Não podem ser definidas relações de chave estrangeira em tabelas publicadas com a opção CASCADE. Para mais informações, consulte [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) e [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).

-   Você não pode atualizar qualquer coluna que é usada na cláusula de relação lógica.

-   A resolução de conflitos personalizada com manipuladores de lógica de negócios ou resolvedores personalizados não tem suporte para artigos que não são incluídos em um registro lógico.

-   Se registros lógicos forem usados em uma publicação que inclui filtros com parâmetros, você deverá inicializar cada Assinante com um instantâneo de sua partição. Se você inicializar um Assinante com outro método, o Merge Agent falhará. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../snapshots-for-merge-publications-with-parameterized-filters.md).

-   Não são exibidos conflitos que envolvem registros lógicos no Visualizador de Conflitos. Para exibir informações sobre esses conflitos, use procedimentos armazenados de replicação. Para obter mais informações, consulte [Exibir informações sobre conflitos em publicações de mesclagem &#40;Programação Transact-SQL de replicação&#41;](../view-conflict-information-for-merge-publications.md).

### <a name="publication-settings"></a>Configurações de Publicação

-   A publicação deve ter um nível de compatibilidade de 90RTM ou maior. Para mais informações, consulte a seção "Nível de Compatibilidade para publicações” em [Compatibilidade com a replicação](../replication-backward-compatibility.md).

-   A publicação deve usar modo de instantâneo nativo. Este é o padrão a menos que você esteja replicando para [!INCLUDE[ssEW](../../../includes/ssew-md.md)], que não oferece suporte a registros lógicos.

-   A publicação não pode permitir sincronização da Web. Para obter mais informações sobre a sincronização da Web, consulte [Web Synchronization for Merge Replication](../web-synchronization-for-merge-replication.md).

-   Para usar registros lógicos em uma publicação filtrada:

    -   Também devem ser usadas partições pré-computadas. Os requisitos de partições pré-computadas também se aplicam a registros lógicos. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).

    -   Você não pode usar filtros com parâmetros que não se sobrepõem. Para obter mais informações, consulte a seção "Configurando opções de partição" em [Filtros de linha com parâmetros](parameterized-filters-parameterized-row-filters.md).

-   Se a publicação usar filtros de junções, a propriedade **juntar chave exclusiva** deverá ser definida como **verdadeiro** para todos os filtros de junção que são envolvidos em relações de registro lógico. Para obter mais informações, consulte [Join Filters](join-filters.md).

### <a name="relationships-between-tables"></a>Relações entre tabelas

-   Tabelas relacionadas por registros lógicos devem ter uma relação chave primária-chave estrangeira.

-   A opção NOT FOR REPLICATION não pode ser definida para restrições de chave estrangeira.

-   Tabelas filho podem ter só uma tabela pai.

     Por exemplo, um banco de dados que rastreia classes e estudantes poderá ter um design semelhante a:

     ![Tabela filho com mais de uma tabela pai](../media/logical-records-03.gif "Tabela filho com mais de uma tabela pai")

     Você não pode usar um registro lógico para representar as três tabelas nessa relação, porque as linhas em **ClassMembers** não são associadas com uma linha de chave primária única. As tabelas **Classes** e **ClassMembers** poderiam ainda formar um registro lógico, como poderiam as tabelas **ClassMembers** e **Students**, mas não todas as três.

-   A publicação não pode conter relações de filtro de junção circulares.

     Usando o exemplo com as tabelas **Customers**, **Orders**e **OrderItems**, você não poderia usar registros lógicos se a tabela **Orders** também tivesse uma restrição de chave estrangeira que fez referência à tabela **OrderItems** .

## <a name="performance-implications-of-logical-records"></a>Implicações de desempenho de registros lógicos
 O recurso de registro lógico vem com um custo de desempenho. Se não forem usados registros lógicos, o agente de replicação poderá processar todas as alterações para um determinado artigo ao mesmo tempo, e como as alterações são aplicadas no modo linha por linha, os requisitos de bloqueio e log de transação, necessários para aplicar as alterações, serão mínimos.

 Se registros lógicos forem usados, o Merge Agent deverá processar as alterações para cada registro lógico inteiro, de forma conjunta. Isto tem um efeito no tempo necessário para o Merge Agent replicar as linhas. Adicionalmente, como o agente abre uma transação separada para cada registro lógico, os requisitos de bloqueio podem aumentar.

## <a name="see-also"></a>Consulte Também
 [Opções de artigo para replicação de mesclagem](article-options-for-merge-replication.md)


