---
title: Configurações (conversão) (MySQLToSQL) do projeto | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-mysql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 7ad5fe44-6445-4ba8-a457-5af792631f11
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: fea682853913c79a82bcd70a25ef24af287eb6f6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="project-settings-conversion-mysqltosql"></a>Configurações de projeto (conversão) (MySQLToSQL)
A página de conversão do **configurações de projeto** caixa de diálogo contém configurações que personalizam como o SSMA converte a sintaxe do MySQL a sintaxe de SQL Server ou SQL Azure.  
  
O painel de conversão está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo.  
  
-   Use o **configurações de projeto padrão** caixa de diálogo para definir opções de configuração para todos os projetos. Para acessar as configurações de conversão no **ferramentas** menu, selecione **configurações de projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido e alterado de **versão de destino de migração** lista suspensa, clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **conversão**.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu clique **configurações de projeto**, em seguida, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **conversão**.  
  
## <a name="options"></a>Opções  
  
### <a name="collate-clause"></a>Cláusula de agrupamento  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Conversão explícita de cláusula COLLATE**|Opção de conversão de cláusula COLLATE explícita Especifica a conversão explícitas cláusulas COLLATE em código do MySQL. Opções possíveis: Ignorar e marcar um aviso / gera um erro<br /><br />**Modo padrão**: ignorar e marca com um aviso<br /><br />**Modo otimista**: ignorar e marca com um aviso<br /><br />**Modo de inteira**: ignorar e marca com um aviso|  
  
### <a name="column-constraints"></a>Restrições de coluna  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Gerar restrição para colunas do tipo de dados ENUM**|Gera a restrição para colunas do tipo de dados de Enumeração na tabela do SQL Server ou SQL Azure, se ele não está presente na tabela de MySQL. Se Sim, todas as colunas convertidas do tipo de dados ENUM serão acompanhadas de controlar o valor de restrição de verificação.<br /><br />**Modo padrão**: nenhuma<br /><br />**Modo otimista**: nenhuma<br /><br />**Modo de inteira**: Sim|  
|**Gerar restrição para colunas do tipo de conjunto de dados**|Gera a restrição para colunas do tipo de conjunto de dados na tabela do SQL Server ou SQL Azure, se ele não está presente na tabela de MySQL. Se Sim, todas as colunas convertidas do tipo de conjunto de dados serão acompanhadas de controlar o valor de restrição de verificação.<br /><br />**Modo padrão**: nenhuma<br /><br />**Modo otimista**: nenhuma<br /><br />**Modo de inteira**: Sim|  
|**Gerar restrição para colunas de colunas do tipo de dados numérico não assinado**|Adicione seleção de valor não negativo para as colunas de tipos de dados numérico não assinado.<br /><br />**Modo padrão**: nenhuma<br /><br />**Modo otimista**: nenhuma<br /><br />**Modo de inteira**: Sim|  
|**Gerar restrição para colunas de tipo de dados do ano**|Gera a restrição para colunas de tipo de dados do ano na tabela do SQL Server ou SQL Azure, se ele não está presente na tabela de MySQL. Em caso afirmativo, todos convertidos de colunas de dados do ano tipo será acompanhado de controlar o valor de restrição de verificação.<br /><br />**Modo padrão**: nenhuma<br /><br />**Modo otimista**: nenhuma<br /><br />**Modo de inteira**: Sim|  
  
### <a name="data-types"></a>Tipos de dados  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Conversão de tipo de dados ENUM**|Especifica como o tipo de dados MySQL ENUM deve ser convertido como converter em NVARCHAR ou Convert para numérico<br /><br />**Modo padrão**: converter em NVARCHAR<br /><br />**Modo otimista**: converter em NVARCHAR<br /><br />**Modo de inteira**: converter em NVARCHAR|  
|**Conversão de tipo do conjunto de dados**|Especifica como o tipo de dados MySQL definido deve ser convertido, converta para NVARCHAR (L) / converter em BINARY(L)<br /><br />**Modo padrão**: converter em NVARCHAR(L)<br /><br />**Modo otimista**: converter em NVARCHAR(L)<br /><br />**Modo de inteira**: converter em NVARCHAR(L)|  
  
### <a name="generic"></a>Genérico  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Colunas sem valor padrão na inserção e substituir**|Se 'Sim', todas as instruções que fazem referência a tabelas usando armazenados mecanismos diferentes MyISAM e InnoDb devem ser marcadas com mensagens de aviso de conversão.<br /><br />**Modo padrão**: adicionar a lista de colunas<br /><br />**Modo otimista**: adicionar a lista de colunas<br /><br />**Modo de inteira**: adicionar a lista de colunas|  
|**Divisão por Zero produz de conversão**|Especifica se deve ou não emular MySQL sem comportamento ERROR_FOR_DIVISION_BY_ZERO.<br /><br />**Modo padrão**: erro<br /><br />**Modo otimista**: erro<br /><br />**Modo de inteira**: nulo|  
|**Operador IN**|Especifica como converter o operador IN MySQL.<br /><br />**Modo padrão**: sempre converter em<br /><br />**Modo otimista**: sempre converter em<br /><br />**Modo de inteira**: expanda se necessário|  
|**Conversão de função do MySQL**|Especifica como converter as funções padrão do MySQL.<br /><br />**Modo padrão**: otimista<br /><br />**Modo otimista**: otimista<br /><br />**Modo de inteira**: preciso|  
|**Não tem suporte a mecanismos de armazenamento**|Se 'Sim', todas as instruções que fazem referência a tabelas usando armazenados mecanismos diferentes MyISAM e InnoDb devem ser marcadas com mensagens de aviso de conversão.<br /><br />**Modo padrão**: nenhuma<br /><br />**Modo otimista**: nenhuma<br /><br />**Modo de inteira**: Sim|  
|**Suprimir a geração de coluna auxiliar ROWID**|Em caso afirmativo, impede a criação de criação de coluna auxiliar ROWD nas tabelas de destino. Pode afetar a migração de algumas estruturas.<br /><br />**Modo padrão**: nenhuma<br /><br />**Modo otimista**: nenhuma<br /><br />**Modo de inteira**: nenhuma|  
|**Conversão de instrução TRUNCATE**|Especifica como converter instruções TRUNCATE.<br /><br />**Modo padrão**: TRUNCATE<br /><br />**Modo otimista**: TRUNCATE<br /><br />**Modo de inteira**: TRUNCATE|  
  
### <a name="misc"></a>Diversos  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Mapeamento de esquema padrão**|Especifica como mapear os bancos de dados MySQL em esquemas do SQL Server.<br /><br />**Modo padrão**: banco de dados no banco de dados<br /><br />**Modo otimista**: banco de dados no banco de dados<br /><br />**Modo de inteira**: banco de dados no banco de dados|  
  
### <a name="procedures-and-functions"></a>Procedimentos e Funções  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Conversão de função padrão**|Especifica se funções deve ser convertido, por padrão para funções T-SQL ou procedimentos armazenados.<br /><br />**Modo padrão**: converter em função<br /><br />**Modo otimista**: converter em função<br /><br />**Modo de inteira**: converter em função|  
|**Gerar SET XACT_ABORT**|Especifica se SET XACT_ABORT ON precisa ser adicionado ao início do procedimento convertido ou gatilho.<br /><br />**Modo padrão**: Sim<br /><br />**Modo otimista**: Sim<br /><br />**Modo de inteira**: Sim|  
|**Gerar SET NOCOUNT em**|Especifica se SET NOCOUNT ON precisa ser adicionado ao início do procedimento convertido ou gatilho.<br /><br />**Modo padrão**: Sim<br /><br />**Modo otimista**: Sim<br /><br />**Modo de inteira**: Sim|  
  
### <a name="spatial-data-types"></a>Tipos de dados espaciais  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Padrão de caixa delimitadora {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} para índices espaciais**|Define o valor padrão para {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} parâmetro usada em índices espaciais de caixa delimitadora.<br /><br />**Modo padrão**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**Modo otimista**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX:  100<br /><br />YMIN: 0<br /><br />**Modo completo**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0|  
|**Densidade padrão da grade para índices espaciais**|Define o valor padrão para LEVEL_1, LEVEL_2, LEVEL_3 e LEVEL_4 de densidade de grade usada em índices espaciais.<br /><br />**Modo padrão**<br /><br />LEVEL_1: padrão<br /><br />LEVEL_2: padrão<br /><br />LEVEL_3: padrão<br /><br />LEVEL_4: padrão<br /><br />**Modo otimista**<br /><br />LEVEL_1: padrão<br /><br />LEVEL_2: padrão<br /><br />LEVEL_3: padrão<br /><br />LEVEL_4: padrão<br /><br />**Modo completo**<br /><br />LEVEL_1: padrão<br /><br />LEVEL_2: padrão<br /><br />LEVEL_3: padrão<br /><br />LEVEL_4: padrão|  
  
### <a name="transactions"></a>Transactions  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Tabelas não transacional**|Especifica se todas as referências à tabela que não oferecem suporte a transações devem ser marcadas com mensagens de aviso de conversão.<br /><br />**Modo padrão**: nenhuma<br /><br />**Modo otimista**: nenhuma<br /><br />**Modo de inteira**: Sim|  
|**Nível de isolamento da transação**|Especifica o nível de isolamento da transação deve ser usado para novas transações.<br /><br />**Modo padrão**: padrão<br /><br />**Modo otimista**: padrão<br /><br />**Modo de inteira**: leitura repetida|  
  
### <a name="value-control"></a>Controle de valor  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Caractere de conversão numérica**|Especifica como lidar com a conversão implícita e explícita de tipo de dados de caractere para tipos de dados numéricos.<br /><br />**Modo padrão**: otimista<br /><br />**Modo otimista**: otimista<br /><br />**Modo de inteira**: preciso|  
|**Controlar valores numéricos não ASSINADOS**|Controle de atribuir valores de parâmetros e variáveis numéricas sem sinal.<br /><br />**Modo padrão**: nenhuma<br /><br />**Modo otimista**: nenhuma<br /><br />**Modo de inteira**: Sim|  
|**Controlar sem sinal de subtração**|Modificar valores negativos inseridos em colunas de tabela de tipo de dados não assinado.<br /><br />**Modo padrão**: converter ' como-está '<br /><br />**Modo otimista**: converter ' como-está '<br /><br />**Modo de inteira**: marca com um aviso|  
|**Conversão de e para o tipo de dados binários**|Especifica como lidar com a conversão implícita e explícita do tipo de dados binários.<br /><br />**Modo padrão**: otimista<br /><br />**Modo otimista**: otimista<br /><br />**Modo de inteira**: preciso|  
|**Tipo de conversão de dados de data/hora**|Especifica como lidar com a conversão implícita e explícita de data/hora de tipo de dados.<br /><br />**Modo padrão**: formato de emular MySQL<br /><br />**Modo otimista**: formato Use SQL Server<br /><br />**Modo de inteira**: formato emular MySQL|  
|**Literais numéricos com precisão exceder 38**|Especifica como converter literais numéricos com precisão exceder 38.<br /><br />**Modo padrão**: arredondar se possível<br /><br />**Modo otimista**: arredondar se possível<br /><br />**Modo de inteira**: arredondar se possível|  
|**Data de zero em colunas NULL e não**|Especifica como lidar com a atribuição não NULL colunas da data de Zero, data de Zero ou valores de data/hora inválido.<br /><br />**Modo padrão**: getDate)<br /><br />**Modo otimista**: getDate)<br /><br />**Modo de inteira**: getDate)|  
  
## <a name="see-also"></a>Consulte também  
[Referência da Interface de usuário &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
  
