---
title: Criar diagramas de banco de dados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:65536
- vdt.DatabaseDesigner
helpviewer_keywords:
- Database Diagram Designer
- Visual Database Tools [SQL Server], database diagrams
- database diagrams [SQL Server], designing
- diagrams [SQL Server], designing
ms.assetid: 6d2c14e1-3d73-4d10-ae5b-7f2b5d6c4ea8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e348ace954e19c3e213c7de1779cbfbcb1768887
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52819358"
---
# <a name="design-database-diagrams-visual-database-tools"></a>Criar diagramas de banco de dados (Visual Database Tools)
  O Designer de Banco de Dados é uma ferramenta visual que permite projetar e visualizar um banco de dados ao qual se está conectado. Ao criar um banco de dados, você pode usar o Designer de Banco de Dados para criar, editar ou excluir tabelas, colunas, chaves, índices, relações e restrições. Para visualizar um banco de dados, você pode criar um ou mais diagramas que ilustrem todas ou parte das tabelas, colunas, chaves e relações.  
  
 ![Diagrama de banco de dados mostrando as relações de tabela](../../database-engine/media//dv3w7c1.gif "Diagrama de banco de dados mostrando as relações de tabela")  
  
 De qualquer banco de dado, você pode criar quantos diagramas desejar; cada tabela de banco de dados podendo aparecer em qualquer número de diagramas. Dessa forma, é possível criar diagramas diferentes para visualizar partes diferentes do banco de dados, ou destacar aspectos diferentes do projeto. Por exemplo, você pode criar um diagrama amplo, que mostre todas as tabelas e colunas, e pode criar um diagrama menor, que mostre todas as tabelas sem mostrar as colunas.  
  
 Todo diagrama de banco de dados criado fica armazenado no banco de dados associado.  
  
## <a name="tables-and-columns-in-a-database-diagram"></a>Tabelas e colunas de um diagrama de banco de dados  
 Dentro de um diagrama de banco de dados, cada tabela pode aparecer com três recursos distintos: uma barra de título, um seletor de linha e um conjunto de colunas de propriedade.  
  
 **Barra de Título** A barra de título mostra o nome da tabela  
  
 Se você modificou uma tabela e ainda não a salvou, um asterisco (*) aparecerá no final do nome da tabela, indicando que há alterações ainda não salvas. Para obter informações sobre como salvar tabelas e diagramas alterados, consulte [Trabalhar com diagramas de banco de dados &#40;Visual Database Tools&#41;](visual-database-tools.md)  
  
 **Seletor de linhas** Clique no seletor de linhas para selecionar uma coluna de banco de dados na tabela. O seletor de linhas exibirá um símbolo de chave caso a coluna conste da chave primária da tabela. Para obter informações sobre chaves primárias, consulte [Primary and Foreign Key Constraints](../../relational-databases/tables/primary-and-foreign-key-constraints.md).  
  
 **Colunas de propriedade** O conjunto de colunas de propriedade é visível em algumas exibições de sua tabela. Você pode exibir uma tabela em qualquer uma das cinco exibições diferentes para poder gerenciar o tamanho e o layout do diagrama.  
  
 Para obter mais informações sobre modos de exibição de tabela, consulte [Personalizar a quantidade de informações exibidas em diagramas &#40;Visual Database Tools&#41;](customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md).  
  
## <a name="relationships-in-a-database-diagram"></a>As relações no diagrama de banco de dados  
 Em um diagrama de banco de dados, cada relação pode aparecer com três recursos distintos: pontos de extremidade, estilo de linha e tabelas relacionadas.  
  
 **Pontos de extremidade** Os pontos de extremidade da linha indicam se a relação é de um-para-um ou de um-para-muitos. Se uma relação tiver uma chave em um ponto de extremidade e o dígito oito no outro, trata-se de uma relação um para muitos. Se a relação tiver uma chave em cada ponto de extremidade, trata-se de uma relação um para um.  
  
 **Estilo de linha** A linha em si (não seus pontos de extremidade) indica se o DBMS (sistema de gerenciamento de banco de dados) impõe a integridade referencial para a relação quando novos dados são adicionados à tabela de chave estrangeira. Se a linha parecer sólida, o DBMS imporá a integridade referencial à relação quando houver adição ou modificação de linhas na tabela de chave estrangeira. Se a linha parecer pontilhada, o DBMS não imporá a integridade referencial à relação quando houver adição ou modificação de linhas na tabela de chave estrangeira.  
  
 **Tabelas relacionadas** A linha da relação indica que existe uma relação de chave estrangeira entre uma e outra tabela. Em uma relação um para muitos, a tabela de chave estrangeira é a tabela próxima ao símbolo do dígito oito da linha. Se ambas as extremidades da linha estiverem anexadas à mesma tabela, trata-se de uma relação reflexiva. Para obter mais informações, consulte [Desenhar relações reflexivas &#40;Visual Database Tools&#41;](draw-reflexive-relationships-visual-database-tools.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Compreender a propriedade do diagrama de banco de dados &#40;Visual Database Tools&#41;](understand-database-diagram-ownership-visual-database-tools.md)  
  
 [Navegar no Designer de Diagramas de Banco de Dados &#40;Visual Database Tools&#41;](navigate-in-database-diagram-designer-visual-database-tools.md)  
  
 [Configurar o Designer de Diagramas de Banco de Dados &#40;Visual Database Tools&#41;](set-up-database-diagram-designer-visual-database-tools.md)  
  
 [Atualizar diagramas de banco de dados de edições anteriores &#40;Visual Database Tools&#41;](upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
  
 [Abrir o Designer de Diagramas de Banco de Dados &#40;Visual Database Tools&#41;](open-database-diagram-designer-visual-database-tools.md)  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com diagramas de banco de dados &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Trabalhar com tabelas no diagrama de banco de dados &#40;Visual Database Tools&#41;](work-with-tables-in-database-diagram-visual-database-tools.md)   
 [Trabalhar com layout de diagrama &#40;Visual Database Tools&#41;](work-with-diagram-layout-visual-database-tools.md)  
  
  
