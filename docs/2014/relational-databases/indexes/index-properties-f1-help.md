---
title: Ajuda de F1 de propriedades do índice | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.indexproperties.storage.f1
- sql12.swb.indexproperties.columns.f1
- sql12.swb.indexproperties.partitions.f1
- sql12.swb.indexproperties.general.f1
- sql12.swb.indexproperties.filter.f1
- sql12.swb.indexproperties.options.f1
- sql12.swb.indexproperties.spatial.f1
ms.assetid: 45efd81a-3796-4b04-b0cc-f3deec94c733
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 390a63d21dc72e052017f2d30b061d71de863bc1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049902"
---
# <a name="index-properties-f1-help"></a>Ajuda de F1 de Propriedades do Índice
  As seções neste tópico referem-se a várias propriedades de índice que estão disponíveis usando caixas de diálogo do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 **Neste tópico:**  
  
 [Página geral das propriedades do índice](#General)  
  
 [Caixa de diálogo Selecionar Colunas (Índice)](#Columns)  
  
 [Página de armazenamento das propriedades do índice](#Storage)  
  
 [Página Espacial das propriedades do índice](#Spatial)  
  
 [Página Filtrar das propriedades do índice](#Filter)  
  
##  <a name="index-properties-general-page"></a><a name="General"></a> Página geral das propriedades do índice  
 Use a página Geral para exibir ou modificar propriedades de índice para a tabela ou exibição selecionada. As opções para cada página podem mudar de acordo com o tipo de índice selecionado.  
  
 **Nome da tabela**  
 Exibe o nome da tabela ou exibição na qual o índice foi criado. Esse campo é somente leitura. Para selecionar uma tabela diferente, feche a página Propriedades do Índice, selecione a tabela correta e, em seguida, abra a página Propriedades do Índice novamente.  
  
 Não é possível especificar índices espaciais em exibições indexadas. Os índices espaciais podem ser definidos apenas em uma tabela com uma chave primária. O número máximo de colunas de chave primária na tabela é 15. O tamanho por linha combinado das colunas de chave primária é limitado a um máximo de 895 bytes.  
  
 **Nome do índice**  
 Exibe o nome do índice. Este campo é somente leitura para um índice existente. Ao criar um novo índice, digite o nome do índice.  
  
 **Tipo de índice**  
 Indica o tipo de índice. Para novos índices, indica o tipo de índice selecionado ao abrir a caixa de diálogo. Os índices podem ser: **Clusterizado**, **Não Clusterizado**, **XML Primário**, **XML Secundário**, **Espacial**, **Columnstore clusterizado**ou **Columnstore não clusterizado**.  
  
 **Observação** É permitido somente um índice clusterizado para cada tabela. É permitido somente um índice columnstore xVelocity de memória otimizada para cada tabela.  
  
 **Exclusivo**  
 A marcação desta caixa de seleção torna o índice exclusivo. Não é permitido que duas linhas tenham o mesmo valor de índice. Por padrão, essa caixa de seleção é desmarcada. Ao modificar um índice existente, haverá falha na criação do índice se duas linhas tiverem o mesmo valor. Para colunas onde NULL é permitido, um índice exclusivo permite um valor NULL.  
  
 Se você selecionar **Espacial** no campo **Tipo de índice** , a caixa de seleção **Exclusiva** ficará esmaecida.  
  
 **Colunas de chave de índice**  
 Adicione as colunas desejadas à grade **Colunas de chave de índice** . Quando mais de uma coluna é adicionada, as colunas devem ser listadas na ordem desejada. A ordem de coluna em um índice pode ter um grande impacto no desempenho do índice.  
  
 Não é permitido que mais de 16 colunas participem de um único índice composto. Para mais de 16 colunas, consulte as colunas incluídas no final deste tópico.  
  
 É possível definir um índice espacial apenas em uma coluna que contenha um tipo de dados espaciais (uma *coluna espacial*).  
  
 **Nome**  
 Exibe o nome da coluna que participa da chave de índice.  
  
 **Sort Order**  
 Especifica a direção da classificação da coluna de índice selecionada, **Crescente** ou **Decrescente**.  
  
> [!NOTE]  
>  Se o tipo de índice for **XML primário** ou **Espacial**, esta coluna não aparecerá na tabela.  
  
 **Tipo de Dados**  
 Exibe a informações de tipo de dados.  
  
> [!NOTE]  
>  Se a coluna de tabela for uma coluna computada, **Tipo de dados** exibirá "coluna computada".  
  
 **Tamanho**  
 Exibe o número máximo de bytes necessários para armazenar o tipo de dados de coluna. Exibe zero (0) para uma coluna espacial ou XML.  
  
 **Identidade**  
 Exibe se a coluna que participa da chave de índice é uma coluna de identidade.  
  
 **Permitir Nulos**  
 Exibe se a coluna que participa da chave de índice permite armazenar valores NULL na tabela ou coluna de exibição.  
  
 **Adicionar**  
 Adiciona uma coluna à chave de índice. Selecione colunas da tabela na caixa de diálogo **selecionar colunas de** , *\<table name>* que aparece quando você clica em **Adicionar**. No caso de um índice espacial, depois que você seleciona uma coluna, este botão fica esmaecido.  
  
 **Remover**  
 Remove a coluna selecionada da participação na chave de índice.  
  
 **Mover para Cima**  
 Move a coluna selecionada para cima na grade de chave de índice.  
  
 **Mover para Baixo**  
 Move a coluna selecionada para baixo na grade de chave de índice.  
  
 **Colunas Columnstore**  
 Clique em **Adicionar** para selecionar colunas para o índice columnstore. Para limitações em um índice columnstore, consulte [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql).  
  
 **Colunas incluídas**  
 Inclua colunas não chave no índice não clusterizado. Essa opção permite ignorar os limites de índices atuais no tamanho total de uma chave de índice e o número máximo de colunas que participam de uma chave de índice, adicionando colunas como colunas não chave no nível folha do índice não clusterizado. Para obter mais informações, consulte [Criar índices com colunas incluídas](create-indexes-with-included-columns.md)  
  
##  <a name="select-index-columns-dialog-box"></a><a name="Columns"></a> Caixa de diálogo Selecionar Colunas (Índice)  
 Use esta página para adicionar colunas à página **Propriedades Gerais do Índice** ao criar ou modificar um índice.  
  
 **Caixa de seleção**  
 Selecione para adicionar colunas.  
  
 **Nome**  
 Nome da coluna.  
  
 **Tipo de Dados**  
 O tipo de dados da coluna.  
  
 **Bytes**  
 Tamanho da coluna em bytes.  
  
 **Identidade**  
 Exibe **Sim** para colunas de identidade e **Não** quando a coluna não é uma coluna de identidade.  
  
 **Permitir Nulos**  
 Exibe **Sim** quando a definição da tabela permitir valores nulos para a coluna. Exibe **Não** quando a definição da tabela não permite nulos para a coluna.  
  
##  <a name="storage-page-options"></a><a name="Storage"></a>Opções de página de armazenamento  
 Use essa página para exibir ou modificar grupo de arquivos ou propriedades de esquema de partição para o índice selecionado. Mostra apenas opções relacionadas ao tipo de índice.  
  
 **Grupo de arquivos**  
 Armazena o índice no grupo de arquivos especificado. A lista exibe apenas grupos de arquivos padrão (linha). A seleção de lista padrão é o grupo de arquivos PRIMARY do banco de dados. Para obter mais informações, consulte [Database Files and Filegroups](../databases/database-files-and-filegroups.md).  
  
 **Grupo de arquivos FILESTREAM**  
 Especifica o grupo de arquivos para obter dados de FILESTREAM. Essa lista exibe apenas grupos de arquivos FILESTREAM. A seleção de lista padrão é o grupo de arquivos PRIMARY FILESTREAM. Para obter mais informações, veja [FILESTREAM &#40;SQL Server&#41;](../blob/filestream-sql-server.md).  
  
 **Esquema de partição**  
 Armazena o índice em um esquema de partição. Clicando em **Esquema de Partição** a grade abaixo é habilitada. A seleção de lista padrão é o esquema de partição usado para armazenar os dados de tabela. Ao selecionar um esquema de partição diferente na lista, a informações na grade é atualizada. Para saber mais, confira [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).  
  
 A opção de esquema de partição fica indisponível se não houver nenhum esquema de partição no banco de dados.  
  
 **Esquema de partição FILESTREAM**  
 Especifica o esquema de partição para dados FILESTREAM. O esquema de partição deve ser simétrico com o esquema especificado na opção **Esquema de partição** .  
  
 Se a tabela não for particionada, o campo fica em branco.  
  
 **Parâmetro do Esquema de Partição**  
 Exibe o nome da coluna que participa do esquema de partição.  
  
 **Coluna de tabela**  
 Selecione a tabela ou exiba para mapear para o esquema de partição.  
  
 **Tipo de dados da coluna**  
 Exibe informações de tipo de dados sobre a coluna.  
  
> [!NOTE]  
>   Se a coluna de tabela for uma coluna computada, **Tipo de Dados da Coluna** exibirá "coluna computada."  
  
 **Permitir o processamento online de instruções DML ao mover o índice**  
 Permite aos usuários acessar a tabela subjacente ou dados de índice clusterizado associados a quaisquer índices não clusterizados durante a operação de índice. Para obter mais informações, consulte [Perform Index Operations Online](perform-index-operations-online.md).  
  
> [!NOTE]  
>  Esta opção não está disponível para índices XML ou se o índice for um índice clusterizadoF desabilitado.  
  
 **Definir grau máximo de paralelismo**  
 Limita o número de processadores a serem usados durante execução do plano paralelo. O valor padrão, 0, usa o número real de CPUs disponíveis. A definição do valor como 1 elimina a geração em plano paralelo; a definição do valor como um número maior que 1 restringe o número máximo de processadores usados por uma única execução da consulta. Esta opção ficará disponível apenas se a caixa de diálogo estiver no estado **Recriar** ou **Recriar** . Para obter mais informações, consulte [definir o Max Degree of Parallelism opção para otimizar o desempenho](../policy-based-management/set-the-max-degree-of-parallelism-option-for-optimal-performance.md).  
  
> [!NOTE]  
>  Se um valor maior que o número de CPUs disponíveis for especificado, será usado o número real de CPUs disponíveis.  
  
##  <a name="spatial-page-index-options"></a><a name="Spatial"></a>Opções de índice da página espacial  
 Use a página **Espacial** para exibir ou especificar os valores das propriedades espaciais. Para obter mais informações, veja [Dados espaciais &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md).  
  
### <a name="bounding-box"></a>Caixa delimitadora  
 A *caixa delimitadora* é o perímetro da grade de alto nível de um plano geométrico. Os parâmetros da caixa delimitadora só existem no mosaico de grade geométrica. Esses parâmetros ficarão indisponíveis se o **Esquema de Mosaico** for **Grade geográfica**.  
  
 O painel exibe as coordenadas **( *`X-min`* , *`Y-min`* )** e **( *`X-max`* , *`Y-max`* )** da caixa delimitadora. Não há valores de coordenada padrão. Portanto, ao criar um novo índice espacial em uma `geometry` coluna de tipo, será necessário especificar os valores de coordenada.  
  
 `X-min`  
 A coordenada X do canto inferior esquerdo da caixa delimitadora.  
  
 `Y-min`  
 A coordenada Y do canto inferior esquerdo da caixa delimitadora.  
  
 `X-max`  
 Coordenada X do canto superior direito da caixa delimitadora.  
  
 `Y-max`  
 Coordenada Y do canto superior direito da caixa delimitadora.  
  
### <a name="general"></a>Geral  
 **Esquema de Mosaico**  
 Indica o esquema de mosaico do índice. Os esquemas de mosaico com suporte são os seguintes:  
  
 **Grade geométrica**  
 Especifica o esquema de mosaico de grade geométrica, que se aplica a uma coluna do tipo de dados `geometry`.  
  
 **Grade Automática de Geometria**  
 Esta opção é habilitada para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando o nível de compatibilidade de banco de dados é definido como 110 ou superior.  
  
 **Grade geográfica**  
 Especifica o esquema de mosaico de grade de geografia, que se aplica a uma coluna do tipo de dados **geografia** .  
  
 **Grade Automática de Geografia**  
 Esta opção é habilitada para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando o nível de compatibilidade de banco de dados é definido como 110 ou superior.  
  
 Para obter informações sobre como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] implementa o mosaico, consulte [Dados espaciais &#40;SQL Server&#41;](../spatial/spatial-data-sql-server.md).  
  
 **Células por Objeto**  
 Indica o número de células por objeto do mosaico que pode ser usado para um único objeto espacial no índice. Esse número pode ser qualquer inteiro entre 1 e 8.192, inclusive. O padrão é 16, e 8 para versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando o nível de compatibilidade de banco de dados é definido como 110 ou superior.  
  
 No nível superior, se um objeto abranger mais células que o especificado por *n*, a indexação usará o número de células necessário para fornecer um mosaico de nível superior completo. Nesses casos, um objeto poderia receber mais que o número de células especificado. Nesse caso, o número máximo de células geradas pela grade de nível superior, que depende da densidade **Nível 1** .  
  
### <a name="grids"></a>Grades  
 Este painel mostra a densidade da grade a cada nível do esquema de mosaico. A densidade é especificada como **Baixa**, **Média**ou **Alta**. O padrão **Média**. **Baixa** representa uma grade de 4x4 (16 células), **Média** representa uma grade de 8x8 (64 células) e **Alta** representa uma grade de 16x16 (256 células). Essas opções não estão disponíveis quando as opções de mosaico **Grade Automática de Geometria** ou **Grade Automática de Geografia** são escolhidas.  
  
 **Nível 1**  
 A densidade da grade de primeiro nível (superior).  
  
 **Nível 2**  
 A densidade da grade de segundo nível.  
  
 **Nível 3**  
 A densidade da grade de terceiro nível.  
  
 **Nível 4**  
 A densidade da grade de quarto nível.  
  
##  <a name="filter-page"></a><a name="Filter"></a>Página de filtro  
 Use esta página para inserir o predicado do filtro para um índice filtrado. Para saber mais, confira [Create Filtered Indexes](create-filtered-indexes.md).  
  
 **Expressão de filtro**  
 Define quais linhas de dados devem ser incluídas no índice filtrado. Por exemplo, `StartDate > '20000101' AND EndDate IS NOT NULL'.`  
  
## <a name="see-also"></a>Consulte Também  
 [Definir opções de índice](set-index-options.md)   
 [INDEXproperty &#40;&#41;Transact-SQL](/sql/t-sql/functions/indexproperty-transact-sql)   
 [sys.indexes &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-indexes-transact-sql)  
  
  
