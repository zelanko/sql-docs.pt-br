---
title: Propriedades da coluna de tabela (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65558
- vdtsql.chm:69657
- vdt.ppg.columns
ms.assetid: 09830897-cc10-46b8-95f5-e0e9681b668c
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a435872914c99990d57804aef0e7e869e1d4737e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="table-column-properties-sql-server-management-studio"></a>Propriedades da coluna de tabela (SQL Server Management Studio)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  As propriedades aparecem no painel inferior do Criador de Tabelas. A menos que seja indicado o contrário, será possível editar as propriedades na janela Propriedades quando a coluna for selecionada. As **Propriedades de Colunas** podem ser exibidas em categorias ou em ordem alfabética. Muitas propriedades aparecem ou podem ser alteradas apenas para certos tipos de dados.  
  
> [!NOTE]  
>  Se a tabela for publicada para replicação, será necessário fazer alterações no esquema usando a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER TABLE [do](../../t-sql/statements/alter-table-transact-sql.md) ou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
 **Geral**  
 Expande para mostrar **Nome**, **Permitir Nulos**, **Tipo de Dados**, **Valor Padrão ou Associação**, **Comprimento**, **Precisão**e **Escala**.  
  
 **Nome**  
 Exibe o nome da coluna selecionada.  
  
 **Permitir Nulos**  
 Indica se essa coluna permite valores nulos. Para editar essa propriedade, clique na caixa de seleção Permitir Nulos que corresponde à coluna no painel superior do Criador de Tabelas.  
  
 **Tipo de Dados**  
 Exibe o tipo de dados para a coluna selecionada. Para editar essa propriedade, clique em seu valor, expanda a lista suspensa e escolha outro valor.  
  
 **Valor Padrão ou Associação**  
 Exibe o padrão para a coluna sempre que nenhum valor for especificado para a mesma. O valor desse campo pode ser o valor de uma restrição padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o nome de uma restrição geral para a qual a coluna será associada. A lista suspensa contém todos os padrões gerais definidos no banco de dados. Para associar a coluna a um padrão geral, faça a seleção na lista suspensa. Alternativamente, para criar uma restrição padrão para a coluna, digite o valor padrão diretamente como texto.  
  
 **Comprimento**  
 Mostra o número de caracteres permitido para tipos de dados com base em caractere. Esta propriedade só está disponível para tipos de dados com base em caractere  
  
 **Escala**  
 Exibe o número de máximo de dígitos que podem aparecer à direita do ponto decimal para valores dessa coluna. Essa propriedade mostra **0** para tipos de dados não numéricos.  
  
 **Precisão**  
 Exibe o número máximo de dígitos para valores nessa coluna. Essa propriedade mostra **0** para tipos de dados não numéricos.  
  
 **Criador de Tabelas**  
 Expande a seção **Designer de Tabela** .  
  
 **Agrupamento**  
 Exibe a sequência de agrupamento que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplica como padrão à coluna, sempre que os valores de coluna forem usados para ordenar as linhas de um resultado de consulta. Para editar o agrupamento, selecione a propriedade, clique na reticência (...) que aparece à direita do valor da propriedade para associar a caixa de diálogo **Agrupamento** .  
  
 **Especificação de Coluna Computada**  
 Exibe informações sobre uma coluna computada. O valor mostrado para propriedade é igual ao valor da propriedade filho **Fórmula** e exibe a fórmula para a coluna computada.  
  
> [!NOTE]  
>  Para alterar o valor mostrado para a propriedade **Especificação de Coluna Computada** , você deve expandi-la e editar a propriedade filho **Fórmula** .  
  
-   A**Fórmula** exibe a fórmula para a coluna computada. Para editar essa propriedade, digite diretamente uma fórmula nova.  
  
-   **Persistente** Indica se os resultados da fórmula foram armazenados. Se essa propriedade for definida como **Não** então, apenas a fórmula será armazenada e os valores serão calculados sempre que a coluna for referenciada. Para editar essa propriedade, clique em seu valor, expanda a lista suspensa e escolha outro valor.  
  
 Para obter mais informações, consulte [Specify Computed Columns in a Table](../../relational-databases/tables/specify-computed-columns-in-a-table.md).  
  
 **Tipo de Dados Condensado**  
 Exibe informações sobre o tipo de dados do campo, no mesmo formato que a instrução SQL CREATE TABLE. Por exemplo, um campo que contém uma cadeia de caracteres de comprimento variável com um comprimento de máximo de 20 caracteres seria representado como "varchar(20)". Para alterar essa propriedade, digite o valor diretamente.  
  
 **Descrição**  
 Exibe o texto que descreve a coluna. Para editar a descrição, selecione a propriedade, clique na reticência (...) que aparece à direita do valor da propriedade e edite a descrição na caixa de diálogo **Descrição da Propriedade** .  
  
 **Determinística**  
 Mostra se o tipo de dados da coluna selecionada pode ser determinado com certeza.  
  
 **Publicado por DTS**  
 Mostra se a coluna é publicada por DTS. ([O Data Transformation Services foi preterido](https://msdn.microsoft.com/library/cc707786(v=sql.130).aspx#Anchor_0)). 
  
 **Especificação de texto completo**  
 Exibe informações sobre um índice de texto completo. O valor dessa propriedade é o valor da propriedade filho **É texto completo indexado** e indica se a coluna é texto completo indexado.  
  
> [!NOTE]  
>  Para alterar o valor mostrado para a propriedade **Especificação de texto completo** , é necessário expandir e editar a propriedade filho **É texto completo indexado** .  
  
-   **É texto completo indexado** Indica se essa coluna é texto completo indexado. Essa propriedade só poderá ser definida como **Sim** se o tipo de dados para essa coluna for pesquisável com texto completo e se a tabela à qual essa coluna pertence tiver um índice de texto completo especificado para isso. Para editar a propriedade, clique no valor correspondente, expanda a lista suspensa e escolha um valor.  
  
-   **Coluna de tipo texto completo** Exibe o nome da coluna, na qual a coluna é de texto completo indexado. Essa propriedade deve ser definida, se a propriedade **Tipo de dados** para a coluna for **imagem** ou **varbinary**. A coluna nomeada na propriedade deve ser de tipo **[n]char, [n]varchar** ou **xml**e a lista suspensa para a propriedade só deve conter colunas que tiverem um desses três tipos de dados. Linhas na coluna nomeada pela propriedade indicam o tipo de documento das linhas correspondentes na coluna pesquisável de texto completo. Para editar essa propriedade, clique em seu valor, expanda a lista suspensa e escolha outro valor.  
  
-   **Idioma** Indica o idioma do separador de palavras usado para indexar a coluna. O valor armazenado na propriedade é o identificador de localidade para o separador de palavras. Para obter mais informações sobre os separadores de palavras e LCIDs, consulte os Separadores de Palavras e os Lematizadores. Para editar essa propriedade, clique em seu valor, expanda a lista suspensa e escolha outro valor.  
  
 **Semântica Estatística**  
 Especifique se habilitará a semântica estatística da coluna selecionada. Para obter mais informações, veja [Pesquisa semântica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
 Se você selecionar um **Idioma** antes de selecionar **Semântica Estatística**, e o idioma selecionado não tiver um Modelo de Idioma Semântico associado, a caixa de seleção **Semântica Estatística** será definida como **Não** e não poderá ser modificada. Se você selecionar **Sim** na opção **Semântica Estatística** antes de selecionar um **Idioma**, os idiomas disponíveis na coluna **Idioma** serão restringidos a esses para os quais o Modelo de Idioma Semântico oferece suporte.  
  
 **Tem Assinante Não SQL Server**  
 Indicar se a coluna está sendo replicada para um assinante que não é um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Especificação de identidade**  
 Exibe informações sobre se e como a coluna impõe exclusividade em seus valores. O valor da propriedade indica se esta coluna é ou não uma coluna de identidade e se é igual ao valor da propriedade filho **É identidade**.  
  
> [!NOTE]  
>  Para alterar o valor mostrado para a propriedade **Especificação de identidade** , é necessário expandir e editar a propriedade filho **É identidade** .  
  
-   **É identidade** Indica se a coluna é ou não uma coluna de identidade. Para editar essa propriedade, clique em seu valor, expanda a lista suspensa e escolha outro valor.  
  
-   **Semente de identidade** Exibe o valor de semente especificado durante a criação desta coluna de identidade. Esse valor é atribuído à primeira linha da tabela. Se essa célula for deixada em branco, o valor 1 será atribuído como padrão. Para editar essa propriedade, digite o valor novo diretamente.  
  
-   **Incremento de identidade** Exibe o valor de incremento especificado durante a criação desta coluna de identidade. Esse valor é o incremento a ser feito em **Semente de identidade** para cada linha subsequente. Se essa célula for deixada em branco, o valor 1 será atribuído como padrão. Para editar essa propriedade, digite o valor novo diretamente.  
  
 **Indexável**  
 Mostra se a coluna selecionada pode ser indexada. Por exemplo, colunas calculadas não determinísticas não podem ser indexadas.  
  
 **Publicado por mesclagem**  
 Mostra se uma coluna é publicada por mesclagem.  
  
 **Não para replicação**  
 Indica se os valores de identidade originais são preservados durante a replicação. Para obter mais informações sobre replicação veja CREATE TABLE. Para editar essa propriedade, clique em seu valor, expanda a lista suspensa e escolha outro valor.  
  
 **Replicado**  
 Mostra se essa coluna é replicada em outro local.  
  
 **RowGuid**  
 Indica se o SQL Server usa a coluna como um ROWGUID. É possível definir esse valor como **Sim** apenas para uma coluna de identidade exclusiva. Para editar essa propriedade, clique em seu valor, expanda a lista suspensa e escolha outro valor.  
  
 **Tamanho**  
 Mostra o tamanho em bytes permitido pelo tipo de dados de coluna. Por exemplo, um tipo de dados nchar pode ter um comprimento de 10 (número de caracteres), mas teria um tamanho de 20 para conjuntos de caracteres de Unicode.  
  
> [!NOTE]  
>  O comprimento de um tipo de dados **(max)** varia para cada linha. **sp_help** retorna (-1) como o comprimento de colunas **(max)** . [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] exibe -1 como o tamanho de coluna.  
  
  
