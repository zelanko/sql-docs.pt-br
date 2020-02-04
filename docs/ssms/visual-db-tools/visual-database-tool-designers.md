---
title: Designers do Visual Database Tool
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- data sources [SQL Server]
- View Designer
- Visual Database Tools [SQL Server]
- Database Diagram Designer
- Query Designer [SQL Server]
- design tools [Visual Database Tools]
- Table Designer
- Visual Database Tools [SQL Server], designers
- Properties window [Visual Database Tools]
ms.assetid: bd0ca68e-6f69-42dd-bcb5-ce511673769c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 183ea6523015835a49e3b9d6c5f3db8786d15551
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75246256"
---
# <a name="visual-database-tool-designers"></a>Designers do Visual Database Tool
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
O Visual Database Tools é uma combinação de ferramentas de design que podem ser usadas para trabalhar com uma fonte de dados. Você pode usá-lo para criar consultas, criar ou modificar uma estrutura de banco de dados ou atualizar dados. As ferramentas são o Designer de Diagrama de Banco de Dados, o Designer de Tabelas e os Designers de Consulta e Exibição.  
  
## <a name="properties-window"></a>Janela Propriedades  
A janela de propriedades não é específica do Visual Database Tools, mas é onde muitas modificações podem ser feitas. Ela mostra as propriedades atuais do item selecionado (como uma tabela) e permite a edição dessas propriedades (tudo, do nome das propriedades até a ordenação de uma coluna). Algumas propriedades podem ser observadas na janela de propriedades, mas devem ser modificadas em outra ferramenta.  
  
## <a name="database-diagram-designer"></a>Designer do Diagrama de Banco de Dados  
O Designer do Diagrama de Bancos de Dados fornece uma janela onde você pode criar, editar e mostrar visualmente tabelas e relações em um banco de dados.  
  
Para exibir o Designer de Diagramas de Bancos de Dados, abra um diagrama existente ou clique com o botão direito do mouse no nó do banco de dados no Pesquisador de Objetos e escolha **Novo Diagrama de Banco de Dados** no menu suspenso.  
  
Quando o designer é aberto, o menu **Diagrama de Banco de Dados** é exibido no menu principal. Esse menu é o ponto de acesso aos recursos especiais do designer.  
  
> [!NOTE]  
> Esse designer trabalha com bancos de dados do Microsoft SQL Server.  
>   
> Essa versão do Visual Database Tools não dá suporte ao Microsoft SQL Server versão 7 e anteriores.  
  
## <a name="table-designer"></a>Criador de Tabelas  
O Designer de Tabela é uma ferramenta visual que permite criar e visualizar uma única tabela em um banco de dados do Microsoft SQL Server a que você está conectado.  
  
O Designer de Tabela tem dois painéis. A área superior mostra uma grade; cada linha da grade descreve uma coluna do banco de dados. Para cada coluna do banco de dados, a grade exibe seus atributos fundamentais: nome de coluna, tipo de dados e configuração permitida por nulls.  
  
A área inferior do Designer de Tabela, a guia Propriedades da Coluna, mostra atributos adicionais para a coluna que estiver realçada na área superior.  
  
No Designer de Tabela, você pode clicar com o botão direito do mouse na seção de grade para acessar as caixas de diálogo em que é possível criar e modificar relações, restrições, índices e chaves da tabela.  
  
Para exibir o Designer de Tabela, abra uma tabela existente ou clique com o botão direito do mouse no nó **Tabelas** no Pesquisador de Objetos e escolha **Adicionar Nova Tabela** no menu suspenso.  
  
Quando o designer é aberto, o menu Designer de Tabela é exibido no menu principal. Esse menu é o ponto de acesso aos recursos especiais do designer.  
  
> [!NOTE]  
> Esse designer trabalha com bancos de dados do Microsoft SQL Server.  
>   
> Essa versão do Visual Database Tools não dá suporte ao Microsoft SQL Server versão 7 e anteriores.  
  
## <a name="query-and-view-designer"></a>Designer de Consulta e Exibição  
O Designer de Consulta e Exibição é de fato duas ferramentas que trabalham de modos bem semelhantes. Algumas das principais diferenças são:  
  
-   As exibições são salvas com o banco de dados enquanto as consultas são salvas com um projeto de banco de dados do Visual Studio.  
  
-   O Designer de Consultas trabalha com praticamente todas as fontes de dados, enquanto o Designer de Exibição só trabalha com o SQL Server.  
  
-   O Designer de Consulta permite que você projete instruções SELECT, INSERT, UPDATE e DELETE DML, enquanto as exibições só podem conter instruções SELECT.  
  
### <a name="view-designer"></a>Designer de Exibição  
O Designer de Exibição permite que você crie e visualize uma exibição existente ou elabore nova em um banco de dados do Microsoft SQL Server a que você está conectado.  
  
O Designer de Exibição tem quatro painéis: o painel Diagrama, o painel Critérios, o painel SQL e o painel Resultados. Para obter informações mais detalhadas sobre cada um desses painéis, consulte [Ferramentas do Designer de Consulta e Exibição &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md).  
  
Para exibir o Designer de Exibição, abra uma exibição existente ou clique com o botão direito do mouse no nó **Exibir** no Pesquisador de Objetos e escolha **Adicionar Nova Exibição** no menu suspenso.  
  
Quando o designer é aberto, o menu **Designer de Consultas** é exibido no menu principal. Esse menu é o ponto de acesso aos recursos especiais do designer.  
  
> [!NOTE]  
> Esse designer trabalha com bancos de dados do Microsoft SQL Server.  
>   
> Essa versão do Visual Database Tools não dá suporte ao Microsoft SQL Server versão 7 e anteriores.  
  
## <a name="see-also"></a>Consulte Também  
[Criar diagramas de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-database-diagrams-visual-database-tools.md)  
[Criar tabelas &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-tables-visual-database-tools.md)  
[Tópicos de instruções de como criar consultas e exibições &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
