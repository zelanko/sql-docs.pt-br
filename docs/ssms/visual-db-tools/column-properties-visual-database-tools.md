---
title: Propriedades de Coluna (Ferramentas de Banco de Dados Visual) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.designers.properties.Column.ColumnIdentitySpec
- vdt.designers.properties.Column
- vdt.tablecolumn
- vdt.designers.properties.Column.ColumnComputedColumnSpec
- vdt.designers.properties.Column.ColumnFulltextSpec
ms.assetid: e549a2a8-4154-4ec8-b146-614564169b39
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2e43a42c781ae0133f7d1644d6ea0c82e3197bef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="column-properties-visual-database-tools"></a>Propriedades de Coluna (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Existem dois conjuntos de propriedades para colunas: um conjunto completo que pode ser visualizado na guia **Propriedades da Coluna** no Designer de Tabela (disponível somente para bancos de dados do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ) e um subconjunto que pode ser visualizado na janela Propriedades usando o Gerenciador de Servidores.  
  
> [!NOTE]  
> As propriedades desse tópico são classificadas por categoria e não em ordem alfabética.  
  
> [!NOTE]  
> As caixas de diálogo e os comandos de menu encontrados podem diferir daqueles descritos na Ajuda, dependendo das configurações ativas ou edição. Para alterar suas configurações, selecione **Importar e Exportar Configurações** no menu **Ferramentas** .  
  
## <a name="properties-window"></a>Janela Propriedades  
Essas propriedades aparecem na janela Propriedades quando você seleciona a coluna em Gerenciador de Servidores.  
  
> [!NOTE]  
> Essas propriedades, acessadas usando-se o Gerenciador de Servidores, são somente leitura. Para editar as propriedades da coluna para bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , selecione a coluna no Designer de Tabela. Essas propriedades são descritas mais adiante neste tópico.  
  
**Categoria de identidade**  
Expande para mostrar o **Nome** e propriedades de **Banco de dados** .  
  
**Nome**  
Mostra o nome da coluna.  
  
**Backup de banco de dados**  
Mostra o nome da fonte dos dados para a coluna selecionada. (Aplica-se somente a OLE DB.)  
  
**Categoria Misc**  
Expande para mostrar as propriedades restantes.  
  
**Tipo de Dados**  
Mostra o tipo de dados da coluna selecionada. Para obter mais informações, consulte [Tipos de dados (Transact-SQL)](http://msdn.microsoft.com/en-us/a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4).  
  
**Incremento de Identidade**  
Mostra o incremento a ser adicionado à **Semente de Identidade** para cada linha seguinte da coluna de identidade. (Aplica-se somente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**Semente de Identidade**  
Mostra o valor da semente atribuído à primeira linha da tabela para a coluna de identidade. (Aplica-se somente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**É Identidade**  
Mostra se a coluna selecionada é a coluna de identidade para a tabela. (Aplica-se somente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**Comprimento**  
Mostra o número de caracteres permitido para tipos de dados com base em caractere.  
  
**Anulável**  
Mostra se a coluna permite ou não valores nulos.  
  
**Precisão**  
Mostra o número máximo de dígitos permitido para tipos de dados numéricos. Essa propriedade mostra **0** para tipos de dados não numéricos.  
  
**Escala**  
Mostra o número máximo de dígitos que podem aparecer à direita do ponto decimal para tipos de dados numéricos. Esse valor deve ser menor do que ou igual à precisão. Essa propriedade mostra **0** para tipos de dados não numéricos.  
  
## <a name="column-properties-tab"></a>Guia Propriedades da Coluna  
Para acessar essas propriedades, no Gerenciador de Servidores, clique com o botão direito do mouse na tabela à qual a coluna pertence, escolha **Abrir Definição de Tabela**e selecione a linha na grade de tabela em Designer de Tabela.  
  
> [!NOTE]  
> Essas propriedades só se aplicam a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Categoria Geral**  
Expande para mostrar **Nome**, **Permitir Nulos**, **Tipo de Dados**, **Valor Padrão ou Associação**, **Comprimento**, **Precisão**e **Escala**.  
  
**Nome**  
Exibe o nome da coluna. Para editar o nome, digite-o na caixa de texto.  
  
> [!CAUTION]  
> Se as consultas, exibições, funções definidas pelo usuário, procedimentos armazenados ou programas existentes se referirem à coluna, a alteração de nome tornará esses objetivos inválidos.  
  
**Permitir Nulos**  
Mostra se o tipo de dados da coluna permite ou não valores nulos.  
  
**Tipo de Dados**  
Mostra o tipo de dados para a coluna selecionada. Para editar essa propriedade, clique em seu valor, expanda a lista suspensa e escolha outro valor. Para obter mais informações, consulte [Tipos de dados (Transact-SQL)](http://msdn.microsoft.com/en-us/a54f7373-b247-4d61-8fb8-7f2ec7a8d0a4).  
  
**Valor Padrão ou Associação**  
Mostra o padrão para essa coluna quando nenhum valor for especificado para essa coluna. A lista suspensa contém todos os padrões gerais definidos na fonte de dados. Para associar a coluna a um padrão geral, faça a seleção na lista suspensa. Alternativamente, para criar uma restrição padrão para a coluna, digite o valor padrão diretamente como texto.  
  
**Comprimento**  
Mostra o número de caracteres permitido para tipos de dados com base em caractere. Essa propriedade só fica disponível para tipos de dados baseados em caractere.  
  
**Precisão**  
Mostra o número máximo de dígitos permitido para tipos de dados numéricos. Essa propriedade mostra **0** para tipos de dados não numéricos. Essa propriedade só fica disponível para tipos de dados numéricos.  
  
**Escala**  
Mostra o número máximo de dígitos que podem aparecer à direita do ponto decimal para tipos de dados numéricos. Esse valor deve ser menor do que ou igual à precisão. Essa propriedade mostra **0** para tipos de dados não numéricos. Essa propriedade só fica disponível para tipos de dados numéricos.  
  
**Categoria do Designer de Tabelas**  
Expande para mostrar as propriedades restantes.  
  
**Agrupamento**  
Mostra a configuração de agrupamento da coluna selecionada. Para alterar a configuração, clique em **Agrupamento** e, então, clique nas reticências **(…)** à direita do valor.  
  
**Categoria Especificação de Coluna Computada**  
Expande para mostrar propriedades para **Fórmula** e **É Persistido**. Se a coluna for computada, a fórmula também será exibida. Para editar a fórmula, expanda essa categoria e edite na propriedade **Fórmula** .  
  
**Fórmula**  
Mostra a fórmula que a coluna selecionada usa se for uma coluna computada. Nesse campo é possível digitar ou alterar uma fórmula.  
  
**É Persistido**  
É possível salvar a coluna computada com a fonte de dados. É possível indexar uma coluna computada persistente.  
  
**Tipo de Dados Condensado**  
Exibe informações sobre o tipo de dados do campo, no mesmo formato que a instrução SQL CREATE TABLE. Por exemplo, um campo que contém uma cadeia de caracteres de comprimento-variável com um comprimento máximo de 20 caracteres seria representado como "varchar(20).” Para alterar essa propriedade, digite o valor diretamente.  
  
**Descrição**  
Mostra a descrição da coluna. Para ver a descrição completa ou editá-la, clique em Descrição e, então, clique nas reticências **(…)** à direita da propriedade.  
  
**Categoria Especificação de Texto Completo**  
Expande para mostrar propriedades específicas para colunas de texto completo.  
  
**É Indexado com Texto Completo**  
Indica se essa coluna é indexada com texto completo. Essa propriedade só poderá ser definida como **Sim** se o tipo de dados para essa coluna for pesquisável com texto completo e se a tabela à qual essa coluna pertence tiver um índice de texto completo especificado para isso. Para alterar esse valor, clique nele, expanda a lista suspensa e escolha um valor novo.  
  
**Coluna de tipo de texto completo**  
Mostra que coluna é usada para definir o tipo de documento de uma coluna do tipo imagem. O tipo de dados de imagem pode ser usado para armazenar documentos que variam de arquivos .doc a arquivos a xml.  
  
**Idioma**  
Indica a linguagem usada para indexar a coluna.  
  
**Semântica Estatística**  
Especifique se habilitará a semântica estatística da coluna selecionada. Para obter mais informações, consulte [Espaço reservado Pesquisa semântica](http://msdn.microsoft.com/en-us/cd8faa9d-07db-420d-93f4-a2ea7c974b97).  
  
Se você selecionar um **Idioma** antes de selecionar **Semântica Estatística**, e o idioma selecionado não tiver um Modelo de Idioma Semântico associado, a caixa de seleção **Semântica Estatística** será definida como **Não** e não poderá ser modificada. Se você selecionar **Sim** na opção **Semântica Estatística** antes de selecionar um **Idioma**, os idiomas disponíveis na coluna **Idioma** serão restringidos a esses para os quais o Modelo de Idioma Semântico oferece suporte.  
  
**Tem Assinante Não SQL Server**  
Mostra se a coluna tem um assinante não Microsoft SQL Server.  
  
**Categoria Especificação de Identidade**  
Expande para mostrar propriedades para **É Identidade**, **Incremento de Identidade**e **Semente de Identidade**.  
  
**É Identidade**  
Mostra se a coluna selecionada é a coluna de identidade para a tabela. Para alterar a propriedade, abra a tabela em Designer de Tabela e edite as propriedades na janela **Propriedades** . Essa configuração se aplica apenas a colunas com um tipo de dados baseado em número, como *int*.  
  
**Incremento de Identidade**  
Mostra o incremento que será adicionado à **Semente de Identidade** para cada linha seguinte. Se essa célula for deixada em branco, o valor 1 será atribuído como padrão. Para editar essa propriedade, digite o valor novo diretamente.  
  
**Semente de Identidade**  
Mostra o valor atribuído à primeira linha da tabela. Se essa célula for deixada em branco, o valor 1 será atribuído como padrão. Para editar essa propriedade, digite o valor novo diretamente.  
  
**É Determinístico**  
Mostra se o tipo de dados da coluna selecionada pode ser determinado com certeza.  
  
**É publicado por DTS**  
Mostra se a coluna é publicada por DTS.  
  
**É Indexável**  
Mostra se a coluna selecionada pode ser indexada. Por exemplo, colunas calculadas não determinísticas não podem ser indexadas.  
  
**É Publicado por Mesclagem**  
Mostra se uma coluna é publicada por mesclagem.  
  
**Não é para Replicação**  
Indica se os valores de identidade originais são preservados durante a replicação. Para editar essa propriedade, clique em seu valor, expanda a lista suspensa e escolha outro valor.  
  
**É Replicável**  
Mostra se essa coluna é replicada em outro local.  
  
**É RowGuid**  
Indica se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usa a coluna como ROWGUID. Esse valor pode ser definido como **Sim** somente para uma coluna com o tipo de dados **uniqueidentifier**. Para editar essa propriedade, clique em seu valor, expanda a lista suspensa e escolha outro valor.  
  
**Tamanho**  
Mostra o tamanho em bytes permitido pelo tipo de dados de coluna. Por exemplo, um tipo de dados **nchar** pode ter um comprimento de 10 (número de caracteres), mas teria um tamanho de 20 para conjuntos de caracteres de Unicode.  
  
> [!NOTE]  
> O comprimento de um tipo de dados **varchar(max)** varia para cada linha. sp_help retorna (-1) como o comprimento de colunas **varchar(max)** . [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)] exibe -1 como o tamanho de coluna.  
  
