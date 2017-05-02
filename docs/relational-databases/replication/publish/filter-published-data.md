---
title: Filtrar dados publicados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filters [SQL Server replication]
- filters [SQL Server replication], about filtering
- filtering [SQL Server replication]
- static row filters
- transactional replication, filtering published data
- replication [SQL Server], filtering published data
- filtering published data [SQL Server replication]
- snapshot replication [SQL Server], filtering published data
- column filters [SQL Server replication]
ms.assetid: 8a914947-72dc-4119-b631-b39c8070c71b
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b789fc6033b70608ca30cfa3895442be44ce1e40
ms.lasthandoff: 04/11/2017

---
# <a name="filter-published-data"></a>Filtrar dados publicados
  Filtrar artigos de tabela lhe permite criar partições de dados a serem publicados. Filtrando dados publicados, você pode:  
  
-   Minimizar a quantidade de dados enviada pela rede.  
  
-   Reduzir a quantidade de espaço de armazenamento requerida no Assinante.  
  
-   Personalizar publicações e aplicativos com base em requisitos de Assinante individuais.  
  
-   Evitar ou reduzir conflitos se o Assinante estiver atualizando dados, porque partições diferentes de dados podem ser enviadas a Assinantes diferentes (dois Assinantes não estarão atualizando os mesmos valores de dados).  
  
-   Evitar transmitir dados confidenciais. Podem ser usados filtros de linha e filtros de coluna para restringir um acesso de Assinante aos dados. Para a replicação de mesclagem, haverá considerações de segurança se você usar um filtro com parâmetros que inclua HOST_NAME(). Para obter mais informações, consulte a seção "Filtrando com HOST_NAME()" em [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 A replicação oferece quatro tipos de filtros:  
  
-   Filtros de linha estáticos, que estão disponíveis com todos os tipos de replicação.  
  
     Ao usar filtros de linha estáticos é possível escolher um subconjunto de linhas a ser publicado. Todos os Assinantes para uma publicação filtrada recebem o mesmo subconjunto de linhas para a tabela filtrada. Para obter mais informações, consulte a seção “Filtros de linha estatísticos”, neste tópico.  
  
-   Filtros de coluna, que estão disponíveis com todos os tipos de replicação.  
  
     Ao usar filtros de coluna é possível escolher um subconjunto de colunas a ser publicado. Para obter mais informações, consulte a seção “Filtros de coluna”, neste tópico.  
  
-   Filtros de linha com parâmetros, que estão disponíveis apenas com replicação de mesclagem.  
  
     Ao usar filtros com parâmetros é possível escolher um subconjunto de linhas a ser publicado. Ao contrário de filtros estáticos que enviam o mesmo subconjunto de linhas para cada Assinante, filtros de linhas com parâmetros usam um valor de dados fornecido pelo Assinante para que se envie aos Assinantes diferentes subconjuntos de linhas. Para obter mais informações, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Filtros de junção, que estão disponíveis apenas com replicação de mesclagem.  
  
     Ao usar filtros de junção é possível estender um filtro de linha de uma tabela publicada para outra. Para obter mais informações, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
## <a name="static-row-filters"></a>filtros de linha estáticos  
 A ilustração a seguir mostra uma tabela publicada que é filtrada de forma que apenas as linhas 2, 3 e 6 são incluídas na publicação.  
  
 ![Filtragem de linha](../../../relational-databases/replication/publish/media/repl-16.gif "Filtragem de linha")  
  
 Um filtro de linha estático usa a cláusula WHERE para selecionar os dados apropriados a serem publicados; você especifica a parte final da cláusula WHERE. Considere a tabela **Product** no banco de dados de exemplo Adventure Works, que contém a coluna **ProductLine**. Para publicar somente as linhas com dados em produtos relacionados a mountain bikes, especifique `ProductLine = 'M'`.  
  
 Um filtro de linha estático resulta em um único conjunto de dados para cada publicação. No exemplo anterior, todos os Assinantes receberiam somente as linhas com dados em produtos relacionados a mountain bikes. Se você tiver outro Assinante que exija somente as linhas com dados sobre produtos relacionados a bicicletas de estrada:  
  
-   Com replicação de instantâneo ou transacional, é possível criar outra publicação e incluir a tabela em ambas as publicações (na cláusula de filtro para o artigo naquela publicação, especifique `ProductLine = 'R')`.  
  
    > [!NOTE]  
    >  Filtros de linha em publicações transacionais podem adicionar uma sobrecarga significativa por que a cláusula de filtragem de artigo é avaliada para cada linha de log gravada para uma tabela publicada a fim de determinar se a linha deve ser replicada. Filtros de linha em publicações transacionais devem ser evitados se cada nó de replicação puder dar suporte a toda a carga de dados, e o conjunto completo de dados for relativamente pequeno.  
  
-   Com replicação de mesclagem, use filtros de linha com parâmetro em vez de criar várias publicações com filtros de linha estáticos. Para obter mais informações, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Para definir ou modificar um filtro de linha estático, consulte [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md).  
  
## <a name="column-filters"></a>Filtros de coluna  
 A ilustração a seguir mostra uma publicação que filtra a coluna C.  
  
 ![Filtragem de coluna](../../../relational-databases/replication/publish/media/repl-17.gif "Filtragem de coluna")  
  
 É possível também usar filtragem de linha e coluna juntas, conforme aqui ilustrado.  
  
 ![Filtragem de linha e coluna](../../../relational-databases/replication/publish/media/repl-18.gif "Filtragem de linha e coluna")  
  
 Após a criação de uma publicação é possível usar a filtragem de coluna para cancelar uma coluna de uma publicação existente, mas retendo a coluna na tabela no Publicador, e também incluir uma coluna existente na publicação. Para outras alterações, como a adição de uma nova coluna a uma tabela e, então, a adição dela ao artigo publicado, use replicação de alteração de esquema. Para mais informações, consulte as seções "Adicionando colunas" e "Removendo colunas" no tópico [Fazer alterações em esquemas nos bancos de dados de publicação](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
 Os tipos de colunas listados na tabela a seguir não podem ser filtrados em determinados tipos de publicações.  
  
|Tipo de coluna|Tipo de publicação e opções|  
|-----------------|-------------------------------------|  
|Coluna de chave primária|Colunas de chave primária são exigidas para todas as tabelas em publicações transacionais. Chaves primárias não são exigidas para tabelas em publicações de mesclagem, mas se uma coluna de chave primária estiver presente, ela não pode ser filtrada.|  
|Coluna de chave estrangeira|Todas as publicações criadas usando-se o assistente para Nova Publicação. Você pode filtrar colunas de chave estrangeira usando procedimentos armazenados da Transact-SQL. Para obter mais informações, [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).|  
|A coluna **rowguid**|Publicações de mesclagem*|  
|A coluna **msrepl_tran_version**|Publicações de instantâneo ou transacionais que permitem assinaturas atualizáveis|  
|Colunas que não permitem NULL e não têm valores padrão ou a propriedade IDENTITY definida.|Publicações de instantâneo ou transacionais que permitem assinaturas atualizáveis|  
|Colunas com restrições ou índices exclusivos|Publicações de instantâneo ou transacionais que permitem assinaturas atualizáveis|  
|Todas as colunas em uma publicação de mesclagem SQL Server 7.0|Colunas não podem ser filtradas em publicações de mesclagem SQL Server 7.0.|  
|Timestamp|Publicações de instantâneo ou transacionais SQL Server 7.0 que permitem assinaturas atualizáveis|  
  
 \*Se você está publicando uma tabela em uma publicação de mesclagem e a tabela já contém uma coluna do tipo de dados **uniqueidentifier** com a propriedade **ROWGUIDCOL** definida, a replicação pode usar essa coluna em vez de criar uma coluna adicional chamada **rowguid**. Nesse caso, a coluna existente deve ser publicada.  
  
 Para definir ou modificar um filtro de coluna, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md).  
  
## <a name="filtering-considerations"></a>Filtrando considerações  
 Lembre-se das seguintes considerações ao filtrar dados:  
  
-   Todas as colunas referenciadas em filtros de linha devem ser incluídas na publicação. Em outras palavras, não se pode usar um filtro de coluna para excluir uma coluna usada em um filtro de linha.  
  
-   Se um filtro for adicionado ou alterado depois de inicializadas as assinaturas, as assinaturas devem ser reinicializadas.  
  
-   O número máximo de bytes permitidos para uma coluna usada em um filtro é 1024 para um artigo em uma publicação de mesclagem e 8000 para um artigo em uma publicação transacional.  
  
-   Colunas com os seguintes tipos de dados não podem ser referenciadas em filtros de linha ou filtros de junção:  
  
    -   **varchar(max) e nvarchar(max)**  
  
    -   **varbinary(max)**  
  
    -   **text e ntext**  
  
    -   **image**  
  
    -   **XML**  
  
    -   **UDT**  
  
-   Replicação transacional lhe permite reproduzir uma exibição indexada como uma exibição ou como uma tabela. Se você reproduzir a exibição como uma tabela, você não poderá filtrar colunas da tabela.  
  
 Os filtros de linha não são criados para funcionar nos bancos de dados. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] restringe intencionalmente a execução de **sp_replcmds** (quais filtros serão executados em) ao proprietário do banco de dados (**dbo**). O **dbo** não tem privilégios de banco de dados. Com a adição de CDC (Change Data Capture) em [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] the **sp_replcmds** preenche as tabelas de controle de alterações com informações que o usuário pode retornar e consultar. Por motivos de segurança, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] restringe a execução dessa lógica de modo que um **dbo** mal-intencionado não possa sequestrar esse caminho de execução. Por exemplo, um **dbo** mal-intencionado pode adicionar gatilhos a tabelas CDC que seriam executadas no contexto do usuário que chama **sp_replcmds**, nesse caso, o Log Reader Agent.  Se a conta que o agente está executando tiver um privilégio mais alto, o **dbo** mal-intencionado poderá escalonar os privilégios dele.  
  
## <a name="see-also"></a>Consulte também  
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
