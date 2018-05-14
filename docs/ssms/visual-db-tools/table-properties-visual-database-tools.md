---
title: Propriedades da tabela (Visual Database Tools) | Microsoft Docs
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
- vdt.tabledesigner
- vdt.designers.properties.Table
ms.assetid: cc392987-1aab-45f5-b5af-a26be53409bf
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1140258639056876b8de6b195f5d6df9a2b69fd6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="table-properties-visual-database-tools"></a>Propriedades da tabela (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Essas propriedades aparecem na janela Propriedades quando você clicar em Designer de Tabela com o botão direito do mouse e selecionar Propriedades. A menos que seja indicado o contrário, é possível editar essas propriedades na janela Propriedades quando a tabela for selecionada.  
  
> [!NOTE]  
> Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](http://msdn.microsoft.com/en-us/f1745145-182d-4301-a334-18f799d361d1) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
## <a name="show-table-properties-in-table-designer"></a>Mostrar propriedades da tabela no Designer de Tabela  
  
> [!NOTE]  
> As propriedades desse tópico são classificadas por categoria e não em ordem alfabética.  
  
**Categoria de identidade**  
Expande para mostrar propriedades para **Nome**, **Descrição**e **Esquema**.  
  
**Nome**  
Exibe o nome da tabela. Para editar o nome, digite-o na caixa de texto.  
  
> [!CAUTION]  
> Se as consultas, exibições, funções definidas pelo usuário, procedimentos armazenados ou programas existentes se referirem à tabela, a modificação do nome tornará esses objetivos inválidos.  
  
**Nome do Banco de Dados**  
Mostra o nome da fonte dos dados para a tabela selecionada.  
  
**Descrição**  
Mostra uma descrição da tabela selecionada. Para ver a descrição inteira ou editá-la, clique na descrição e então clique nas reticências **(...)** à direita da propriedade.  
  
**Esquema**  
Mostra o nome do esquema ao qual essa tabela pertence. (Aplica-se somente ao Microsoft SQL Server)  
  
**Nome do servidor**  
Mostra o nome do servidor para a fonte de dados.  
  
**Categoria do Designer de Tabelas**  
Expande para mostrar propriedades para **Coluna de identidade**, **Indexável**e **É Replicado**.  
  
**Coluna de identidade**  
Mostra a coluna usada como a coluna de identidade da tabela. Para alterar a coluna de identidade, escolha a partir da lista suspensa. Apenas colunas de um tipo de dados numérico serão exibidas na lista.  
  
**Indexável**  
Mostra se a tabela pode ser indexada. Se a tabela não for indexável pode ser porque você não é o proprietário da tabela ou porque a tabela contém colunas com tipos de dados de texto, ntext ou imagem.  
  
**É Replicado**  
Mostra se a tabela é replicada em outro local.  
  
**Categoria de especificação espaço de dados regular**  
Expande para mostrar propriedades para **(Tipo de Espaço de Dados)**, **Grupo de Arquivos ou Nome do Esquema de Partição**e **Lista de Colunas de Partição**.  
  
**(Tipo de Espaço de Dados)**  
Mostra se essa tabela é armazenada usando um grupo de arquivos ou esquema de partição.  
  
**Grupo de Arquivos ou Nome do Esquema de Partição**  
Mostra o nome do grupo de arquivos ou esquema de partição.  
  
**Lista de Colunas de Partição**  
Fornece acesso à caixa de diálogo **Lista de Colunas de Partição** .  
  
**Coluna GUID de Linha**  
Mostra a coluna usada pelo Microsoft SQL Server como a coluna ROWGUID da tabela. Para alterar a coluna ROWGUID , escolha a partir da lista suspensa. (Aplica-se apenas ao SQL Server 7.0 ou superior.)  
  
**Grupo de arquivos de Texto/Imagem**  
Fornece uma lista suspensa da qual você pode escolher o grupo de arquivos para colunas que têm tipos de dados de texto ou de imagem. Se a tabela é armazenada usando-se um esquema de partição, deixe esse espaço em branco.  
  
## <a name="see-also"></a>Consulte Também  
[Projetar tabelas (Ferramentas de Banco de Dados Visual)](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
  
