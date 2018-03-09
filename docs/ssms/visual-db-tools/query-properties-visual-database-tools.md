---
title: Propriedades de consulta (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:69636
- vdt.ppg.querydesigner.query
ms.assetid: 07495669-6ed5-4004-904e-aae1230be5e4
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 310d9c728820be6bc8f31b24cc979dea6ad1f7ec
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="query-properties-visual-database-tools"></a>Propriedades de consulta (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Essas propriedades aparecem na janela Propriedades quando você tem uma consulta aberta no Designer de Exibição e Consulta. A menos que seja indicado o contrário, é possível editar essas propriedades na janela Propriedades.  
  
> [!NOTE]  
> As propriedades neste tópico são ordenadas por categoria e não por ordem alfabética.  
  
## <a name="options"></a>Opções  
**Categoria de identidade**  
Expanda para mostrar o **Nome** da propriedade.  
  
**Nome**  
Mostra o nome da consulta atual. Não pode ser alterado no [!INCLUDE[ssManStudio](../../includes/ssmanstudio_md.md)].  
  
**Database Name**  
Mostra o nome da fonte de dados para a tabela selecionada.  
  
**Nome do servidor**  
Mostra o nome do servidor para a fonte de dados.  
  
**Categoria de Designer de Consulta**  
Expande para mostrar as propriedades restantes.  
  
**Tabela de destino**  
Especifique o nome da tabela na qual você está inserindo dados. Essa lista será exibida se você estiver criando uma consulta de INSERT ou consulta de MAKE TABLE. Para uma consulta de INSERT, selecione um nome de tabela da lista.  
  
Para uma consulta de MAKE TABLE, digite o novo nome de tabela. Para criar uma tabela de destino em outra fonte de dados, especifique um nome de tabela totalmente qualificado, incluindo o nome da fonte de dados de destino, o proprietário (se necessário) e o nome da tabela.  
  
> [!NOTE]  
> O Designer de Consulta não verifica se o nome já está em uso ou se você tem permissão para criar a tabela.  
  
**Valores Distintos**  
Especifique se a consulta filtrará duplicatas no conjunto de resultados. Essa opção é útil quando você estiver usando apenas algumas das colunas da tabela, ou tabelas, e essas colunas possam conter valores duplicados ou, quando o processo de junção de duas ou mais tabelas produz linhas duplicadas no conjunto de resultados. Escolhendo essa opção é equivalente para inserir a palavra DISTINCT na instrução no painel SQL.  
  
**Extensão GROUP BY**  
Especifique quais as opções adicionais de consultas com base nas consultas de agregação estão disponíveis. (Aplica-se somente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].)  
  
**Todas as Colunas de Saída**  
Especifique que todas as colunas de todas as tabelas na consulta atual estarão no conjunto de resultados. Escolhendo essa opção é equivalente para especificar um asterisco (*) em lugar de nomes de coluna individual depois da palavra-chave SELECT na instrução SQL.  
  
**Lista de Parâmetro de Consulta**  
Mostra parâmetros de consulta. Para editar os parâmetros, clique na propriedade e, em seguida, clique nas reticências **(…)** à direita da propriedade. (Aplica-se apenas ao OLE DB genérico.)  
  
**Comentário SQL**  
Mostra uma descrição das instruções SQL. Para ver a descrição inteira ou editá-la, clique na descrição e então clique nas reticências **(…)** à direita da propriedade. Os comentários podem incluir informações como quem usa a consulta e quando são usadas. (Aplica-se apenas aos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 7.0 ou posteriores.)  
  
**Categoria Especificação Top**  
Expanda para mostrar as propriedades **Top**, **Percent**, **Expression**e **With Ties** .  
  
**(Top)**  
Especifique que a consulta incluirá uma cláusula TOP, que retorna apenas as primeiras linhas *n* ou primeiro percentual *n* de linhas no conjunto de resultados. O padrão é que a consulta retorne as primeiras 10 linhas no conjunto de resultados.  
  
Use essa caixa para alterar o número de linhas para retornar ou especificar uma porcentagem diferente. (Aplica-se apenas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou posterior.)  
  
**Expression**  
Especifique o número ou porcentagem de linhas que a consulta retornará. Se você definir **Percentual** como Sim, esse número será a porcentagem de linhas que a consulta retornará; se você definir **Percentual** como Não, ele representará o número de linhas a serem retornadas. (Aplica-se apenas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] versão 7.0 ou posterior.)  
  
**Percent**  
Especifique que a consulta retornará apenas os primeiros porcentuais de linhas *n* no conjunto de resultados. (Aplica-se apenas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] versão 7.0 ou posterior.)  
  
**With Ties**  
Especifique que a exibição incluirá uma cláusula WITH TIES. O WITH TIES é útil se uma exibição incluir uma cláusula ORDER BY e uma cláusula TOP com base em porcentagem. Se essa opção for determinada, e se a porcentagem de corte se encontrar no meio de um conjunto de linhas com valores idênticos na cláusula ORDER BY, a exibição será estendida para incluir todas as respectivas linhas. (Aplica-se apenas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] versão 7.0 ou posterior.)  
  
## <a name="see-also"></a>Consulte Também  
[Consultar com parâmetros &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
