---
title: Criar diagramas de banco de dados (Visual Database Tools) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssms-visual-db
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdtsql.chm:65536
- vdt.DatabaseDesigner
helpviewer_keywords:
- Database Diagram Designer
- Visual Database Tools [SQL Server], database diagrams
- database diagrams [SQL Server], designing
- diagrams [SQL Server], designing
ms.assetid: 6d2c14e1-3d73-4d10-ae5b-7f2b5d6c4ea8
caps.latest.revision: "5"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7afa4c3169353a26660f962f84b20346fdd2680b
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="design-database-diagrams-visual-database-tools"></a>Criar diagramas de banco de dados (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] O Designer de Banco de Dados é uma ferramenta visual que permite projetar e visualizar um banco de dados ao qual você está conectado. Ao criar um banco de dados, você pode usar o Designer de Banco de Dados para criar, editar ou excluir tabelas, colunas, chaves, índices, relações e restrições. Para visualizar um banco de dados, você pode criar um ou mais diagramas que ilustrem todas ou parte das tabelas, colunas, chaves e relações.  
  
![Diagrama de banco de dados mostrando as relações de tabela](../../ssms/visual-db-tools/media/dv3w7c1.gif "Diagrama de banco de dados mostrando as relações de tabela")  
  
De qualquer banco de dado, você pode criar quantos diagramas desejar; cada tabela de banco de dados podendo aparecer em qualquer número de diagramas. Dessa forma, é possível criar diagramas diferentes para visualizar partes diferentes do banco de dados, ou destacar aspectos diferentes do projeto. Por exemplo, você pode criar um diagrama amplo, que mostre todas as tabelas e colunas, e pode criar um diagrama menor, que mostre todas as tabelas sem mostrar as colunas.  
  
Todo diagrama de banco de dados criado fica armazenado no banco de dados associado.  
  
## <a name="tables-and-columns-in-a-database-diagram"></a>Tabelas e colunas de um diagrama de banco de dados  
Dentro de um diagrama de banco de dados, cada tabela pode aparecer com três recursos distintos: uma barra de título, um seletor de linha e um conjunto de colunas de propriedade.  
  
**Barra de Título** A barra de título mostra o nome da tabela  
  
Se você modificou uma tabela e ainda não a salvou, um asterisco (*) aparecerá no final do nome da tabela, indicando que há alterações ainda não salvas. Para obter informações sobre como salvar tabelas e diagramas alterados, consulte [Trabalhar com diagramas de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
**Seletor de linhas** Clique no seletor de linhas para selecionar uma coluna de banco de dados na tabela. O seletor de linhas exibirá um símbolo de chave caso a coluna conste da chave primária da tabela. Para obter informações sobre chaves primários, consulte [Como trabalhar com chaves (Visual Database Tools)](http://msdn.microsoft.com/en-us/31fbcc9f-2dc5-4bf9-aa50-ed70ec7b5bcd).  
  
**Colunas de propriedade** O conjunto de colunas de propriedade é visível em algumas exibições de sua tabela. Você pode exibir uma tabela em qualquer uma das cinco exibições diferentes para poder gerenciar o tamanho e o layout do diagrama.  
  
Para obter mais informações sobre modos de exibição de tabela, consulte [Personalizar a quantidade de informações exibidas em diagramas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/customize-the-amount-of-information-displayed-in-diagrams-visual-database-tools.md).  
  
## <a name="relationships-in-a-database-diagram"></a>As relações no diagrama de banco de dados  
Em um diagrama de banco de dados, cada relação pode aparecer com três recursos distintos: pontos de extremidade, estilo de linha e tabelas relacionadas.  
  
**Pontos de extremidade** Os pontos de extremidade da linha indicam se a relação é de um-para-um ou de um-para-muitos. Se uma relação tiver uma chave em um ponto de extremidade e o dígito oito no outro, trata-se de uma relação um para muitos. Se a relação tiver uma chave em cada ponto de extremidade, trata-se de uma relação um para um.  
  
**Estilo de linha** A linha em si (não seus pontos de extremidade) indica se o DBMS (sistema de gerenciamento de banco de dados) impõe a integridade referencial para a relação quando novos dados são adicionados à tabela de chave estrangeira. Se a linha parecer sólida, o DBMS imporá a integridade referencial à relação quando houver adição ou modificação de linhas na tabela de chave estrangeira. Se a linha parecer pontilhada, o DBMS não imporá a integridade referencial à relação quando houver adição ou modificação de linhas na tabela de chave estrangeira.  
  
**Tabelas relacionadas** A linha da relação indica que existe uma relação de chave estrangeira entre uma e outra tabela. Em uma relação um para muitos, a tabela de chave estrangeira é a tabela próxima ao símbolo do dígito oito da linha. Se ambas as extremidades da linha estiverem anexadas à mesma tabela, trata-se de uma relação reflexiva. Para obter mais informações, consulte [Desenhar relações reflexivas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/draw-reflexive-relationships-visual-database-tools.md).  
  
## <a name="in-this-section"></a>Nesta seção  
[Compreender a propriedade do diagrama de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/understand-database-diagram-ownership-visual-database-tools.md)  
  
[Navegar no Designer de Diagramas de Banco de Dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/navigate-in-database-diagram-designer-visual-database-tools.md)  
  
[Configurar o Designer de Diagramas de Banco de Dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/set-up-database-diagram-designer-visual-database-tools.md)  
  
[Atualizar diagramas de banco de dados de edições anteriores &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/upgrade-database-diagrams-from-previous-editions-visual-database-tools.md)  
  
[Abrir o Designer de Diagramas de Banco de Dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/open-database-diagram-designer-visual-database-tools.md)  
  
## <a name="see-also"></a>Consulte também  
[Trabalhar com diagramas de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
[Trabalhar com tabelas no diagrama de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-tables-in-database-diagram-visual-database-tools.md)  
[Trabalhar com layout de diagrama &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-diagram-layout-visual-database-tools.md)  
  
