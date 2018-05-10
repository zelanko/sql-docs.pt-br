---
title: Criar, modificar e remover índices espaciais | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: spatial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-spatial
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], creating
- spatial indexes [SQL Server], dropping
- spatial indexes [SQL Server], creating
- indexes [SQL Server], dropping
- indexes [SQL Server], modifying
- spatial indexes [SQL Server], modifying
ms.assetid: 00c1b927-8ec5-44cf-87c2-c8de59745735
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7466a59f0f9ae3eed8a348cffc43eea519763856
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-modify-and-drop-spatial-indexes"></a>Criar, modificar e remover índices espaciais
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um índice espacial pode executar determinadas operações com mais eficiência em uma coluna do tipo de dados de **geometry** ou **geography** (uma *coluna espacial*). Mais de um índice espacial pode ser especificado em uma coluna espacial. Por exemplo, isto é útil para indexar diferentes parâmetros de mosaico em uma única coluna.  
  
 Há várias restrições na criação de índices espaciais. Para obter mais informações, consulte [Restrições em índices espaciais](#restrictions) neste tópico.  
  
> [!NOTE]  
>  Para obter informações sobre a relação de índices espaciais com a partição e os grupos de arquivos, consulte a seção "Comentários" em [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
##  <a name="creating"></a> Criando, modificando e removendo índices espaciais  
  
###  <a name="create"></a> Para criar um índice espacial  
 **Para criar um índice espacial com o Transact-SQL**  
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
  
 **Para criar um índice espacial usando a caixa de diálogo Novo Índice no Management Studio**  
 ##### <a name="to-create-a-spatial-index-in-management-studio"></a>Para criar um índice espacial no Management Studio  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados que contém a tabela com o índice especificado e expanda **Tabelas**.  
  
3.  Expanda a tabela para a qual você deseja criar o índice.  
  
4.  Clique com o botão direito do mouse em **Índices** e selecione **Novo Índice**.  
  
5.  No campo **Nome do índice** , digite um nome para o índice.  
  
6.  Na lista suspensa **Tipo de índice** , selecione **Espacial**.  
  
7.  Para especificar a coluna espacial que você deseja indexar, clique em **Adicionar**.  
  
8.  Na caixa de diálogo **Selecionar Colunas de** *\<nome da tabela>*, selecione uma coluna do tipo **geometry** ou **geography** marcando a caixa de seleção correspondente. Todas as outras colunas espaciais se tornam não editáveis. Para selecionar uma coluna espacial diferente, primeiro desmarque a coluna selecionada no momento. Quando terminar, clique em **OK**.  
  
9. Verifique a seleção da coluna na grade **Colunas de chave de índice** .  
  
10. No painel **Selecionar uma página** da caixa de diálogo **Propriedades do Índice** , clique em **Espacial**.  
  
11. Na página **Espacial** , especifique os valores que você deseja usar para as propriedades espaciais do índice.  
  
     Ao criar um índice em uma coluna de tipo **geometry**, você deve especificar as coordenadas **(***X-min***,***Y-min***)** e **(***X-max***,***Y-max***)** da caixa delimitadora. Para obter um índice em uma coluna de tipo **geography** , os campos da caixa delimitadora se tornam somente leitura após você especificar o esquema de mosaico **Grade geográfica** porque o mosaico de grade geográfica não usa uma caixa delimitadora.  
  
     Opcionalmente, é possível especificar valores não padrão para o campo **Células por Objeto** e para a densidade da grade em qualquer nível do esquema de mosaico. O número padrão de células por objeto é 16 para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou 8 para o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ou versão superior, e a densidade padrão da grade é **Média** para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
     Você pode selecionar GEOMETRY_AUTO_GRID ou GEOGRAPHY_AUTO_GRID para o esquema de mosaico no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando GEOMETRY_AUTO_GRID ou GEOGRAPHY_AUTO_GRID é selecionado, as opções de densidade de grade Nível 1, Nível 2, Nível 3 e Nível 4 são desabilitadas.  
  
     Para obter mais informações sobre essas propriedades, consulte [Index Properties F1 Help](../../relational-databases/indexes/index-properties-f1-help.md).  
  
12. Clique em **OK**.  
  
> [!NOTE]  
>  Para criar outro índice espacial na mesma ou em outra coluna espacial, repita as etapas anteriores.  
  
  
 **Para criar um índice espacial usando o Designer de Tabela no Management Studio**  
 ##### <a name="to-create-a-spatial-index-in-table-designer"></a>Para criar um índice espacial no Designer de Tabela  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na tabela para a qual deseja criar um índice espacial e clique em **Design**.  
  
     A tabela é aberta no Designer de Tabela.  
  
2.  Selecione uma coluna **geometry** ou **geography** para o índice.  
  
3.  No menu **Designer de Tabela** , clique em **Índice Espacial**.  
  
4.  Na caixa de diálogo **Índices Espaciais** , clique em **Adicionar**.  
  
5.  Selecione o novo índice na lista **Índice Espacial Selecionado** e, na grade à direita, defina as propriedades do índice espacial. Para obter informações sobre as propriedades, consulte [Caixa de diálogo Índices Espaciais &#40;Visual Database Tools&#41;](http://msdn.microsoft.com/library/4d84239a-68c7-4aa2-8602-2b51dd07260f).  
  
  
###  <a name="alter"></a> Para alterar um índice espacial  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
    > [!IMPORTANT]  
    >  Para alterar opções específicas a um índice espacial, como BOUNDING_BOX ou GRID, é possível usar uma instrução CREATE SPATIAL INDEX que especifique DROP_EXISTING = ON ou descartar o índice espacial e criar um novo. Para obter um exemplo, consulte [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).  
  
-   [Modificar um índice](../../relational-databases/indexes/modify-an-index.md)  
  
-   [Mover um índice existente para um grupo de arquivos diferente](../../relational-databases/indexes/move-an-existing-index-to-a-different-filegroup.md)  
  
  
###  <a name="drop"></a> Para descartar um índice espacial  
 **Para descartar um índice espacial com o Transact-SQL**  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 **Para descartar um índice usando o Management Studio**  
 [Excluir um índice](../../relational-databases/indexes/delete-an-index.md)  
  
 **Para descartar um índice espacial usando o Designer de Tabela no Management Studio**  
 ##### <a name="to-drop-a-spatial-index-in-table-designer"></a>Para descartar um índice espacial no Designer de Tabela  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse no índice espacial que você deseja excluir e clique em **Design**.  
  
     A tabela é aberta no Designer de Tabela.  
  
2.  No menu **Designer de Tabela** , clique em **Índice Espacial**.  
  
     A caixa de diálogo **Índice Espacial** é aberta.  
  
3.  Clique no índice que você deseja excluir na coluna **Índice Espacial Selecionado** .  
  
4.  Clique em **Excluir**.  
  
  
##  <a name="restrictions"></a> Restrições em índices espaciais  
 Um índice espacial pode ser criado apenas em uma coluna do tipo **geometria** ou **geografia**.  
  
### <a name="table-and-view-restrictions"></a>Restrições de tabela e de exibição  
 Índices espaciais podem ser definidos apenas em uma tabela que tenha uma chave primária. O número máximo de colunas de chave primária na tabela é 15.  
  
 O tamanho de máximo de registros de chave de índice é 895 bytes. Tamanhos maiores retornam um erro.  
  
> [!NOTE]  
>  Metadados de chave primária não podem ser alterados enquanto um índice espacial estiver definido em uma tabela.  
  
 Não é possível especificar índices espaciais em exibições indexadas.  
  
### <a name="multiple-spatial-index-restrictions"></a>Várias restrições de índices espaciais  
 É possível criar até 249 índices espaciais em qualquer uma das colunas espaciais em uma tabela com suporte. A criação de mais de um índice espacial na mesma coluna espacial pode ser útil, por exemplo, para indexar diferentes parâmetros de mosaico em uma única coluna.  
  
 É possível criar apenas um índice espacial de cada vez.  
  
### <a name="spatial-indexes-and-process-parallelism"></a>Índices espaciais e paralelismo do processo  
 Uma criação de índice pode usar o paralelismo de processo disponível.  
  
### <a name="version-restrictions"></a>Restrições de versões  
 Os mosaicos espaciais introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] não podem ser replicados para o [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Você deverá usar mosaicos espaciais do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] em índices espaciais quando a compatibilidade com versões anteriores com bancos de dados do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] for um requisito.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
  
