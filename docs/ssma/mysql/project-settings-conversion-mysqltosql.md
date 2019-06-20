---
title: Configurações (conversão) (MySQLToSQL) do projeto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7ad5fe44-6445-4ba8-a457-5af792631f11
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 12e2e61c6b55bf3c549c08f2b090059d674ed83d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162021"
---
# <a name="project-settings-conversion-mysqltosql"></a>Configurações do projeto (conversão) (MySQLToSQL)
A página de conversão do **configurações do projeto** caixa de diálogo contém configurações que personalizam como o SSMA converte a sintaxe do MySQL à sintaxe do SQL Server ou SQL Azure.  
  
O painel de conversão está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo.  
  
-   Use o **configurações de projeto padrão** caixa de diálogo para definir opções de configuração para todos os projetos. Para acessar as configurações de conversão na **ferramentas** menu, selecione **configurações do projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida / alterado de  **Versão de destino de migração** lista suspensa, clique em **gerais** na parte inferior do painel esquerdo e, em seguida, selecione **conversão**.  
  
-   Para especificar configurações para o projeto atual, no **ferramentas** menu, clique em **configurações do projeto**, em seguida, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **Conversão**.  
  
## <a name="options"></a>Opções  
  
### <a name="collate-clause"></a>Cláusula de agrupamento  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Conversão explícita de cláusula COLLATE**|Opção explícita de conversão de cláusula COLLATE Especifica como converter explícitas cláusulas COLLATE em código de MySQL. Opções possíveis: Ignorar e marcar com um aviso / gerar um erro<br /><br />**Modo padrão**:  Ignorar e marca com um aviso<br /><br />**Modo otimista**:  Ignorar e marca com um aviso<br /><br />**Modo de inteira**:  Ignorar e marca com um aviso|  
  
### <a name="column-constraints"></a>Restrições de coluna  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Gerar restrição para colunas do tipo de dados ENUM**|Gera a restrição para colunas do tipo de dados de Enumeração na tabela do SQL Server ou SQL Azure, se ele não estiver presente na tabela MySQL. Se Sim, todas as colunas convertidas do tipo de dados de Enumeração serão acompanhadas de controlar o valor de restrição de verificação.<br /><br />**Modo padrão**:   Não<br /><br />**Modo otimista**:  Não<br /><br />**Modo de inteira**:   Sim|  
|**Gerar restrição para colunas de tipo de conjunto de dados**|Gera a restrição para colunas de tipo de conjunto de dados na tabela do SQL Server ou SQL Azure, se ele não estiver presente na tabela MySQL. Se Sim, todas as colunas convertidas do tipo do conjunto de dados serão acompanhadas de controlar o valor de restrição de verificação.<br /><br />**Modo padrão**:   Não<br /><br />**Modo otimista**:  Não<br /><br />**Modo de inteira**:   Sim|  
|**Gerar restrição para colunas de colunas do tipo de dados numérico não assinado**|Adicione verificação de valor não negativo para colunas de tipos de dados numérico não assinado.<br /><br />**Modo padrão**:   Não<br /><br />**Modo otimista**:  Não<br /><br />**Modo de inteira**:   Sim|  
|**Gerar restrição para colunas de tipo de dados do ano**|Gera a restrição para colunas de tipo de dados do ano na tabela do SQL Server ou SQL Azure, se não estiver presente na tabela de MySQL. Se Sim, todos convertidos de colunas de dados do ano de tipo será acompanhado de controlar o valor de restrição de verificação.<br /><br />**Modo padrão**:   Não<br /><br />**Modo otimista**:  Não<br /><br />**Modo de inteira**:   Sim|  
  
### <a name="data-types"></a>Tipos de dados  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Conversão de tipo de dados ENUM**|Especifica como o tipo de dados MySQL ENUM deve ser convertido como converter para NVARCHAR ou converter em numérico<br /><br />**Modo padrão**:  Converter em NVARCHAR<br /><br />**Modo otimista**:  Converter em NVARCHAR<br /><br />**Modo de inteira**:  Converter em NVARCHAR|  
|**Conversão de tipo do conjunto de dados**|Especifica como o tipo de dados MySQL definida deve ser convertido, converta para NVARCHAR (L) / converter em BINARY(L)<br /><br />**Modo padrão**: Converter em NVARCHAR(L)<br /><br />**Modo otimista**: Converter em NVARCHAR(L)<br /><br />**Modo de inteira**: Converter em NVARCHAR(L)|  
  
### <a name="generic"></a>Genérico  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Colunas sem valor padrão na inserção e substituição**|Se 'Sim', todas as instruções que fazem referência a tabelas usando mecanismos armazenados diferentes MyISAM e InnoDb devem ser marcadas com mensagens de aviso de conversão.<br /><br />**Modo padrão**:  Adicionar à lista de colunas<br /><br />**Modo otimista**:  Adicionar à lista de colunas<br /><br />**Modo de inteira**:   Adicionar à lista de colunas|  
|**Divisão por Zero conversão produz**|Especifica se deve ou não emular MySQL sem comportamento ERROR_FOR_DIVISION_BY_ZERO.<br /><br />**Modo padrão**:   Erro<br /><br />**Modo otimista**:  Erro<br /><br />**Modo de inteira**:   NULL|  
|**Operador IN**|Especifica como converter o operador IN MySQL.<br /><br />**Modo padrão**:   Sempre converter em IN<br /><br />**Modo otimista**:  Sempre converter em IN<br /><br />**Modo de inteira**:   Expanda se necessário|  
|**Conversão de função do MySQL**|Especifica como converter funções padrão do MySQL.<br /><br />**Modo padrão**:   Otimistas<br /><br />**Modo otimista**:  Otimistas<br /><br />**Modo de inteira**:   Preciso|  
|**Não tem suporte a mecanismos de armazenamento**|Se 'Sim', todas as instruções que fazem referência a tabelas usando mecanismos armazenados diferentes MyISAM e InnoDb devem ser marcadas com mensagens de aviso de conversão.<br /><br />**Modo padrão**:   Não<br /><br />**Modo otimista**:  Não<br /><br />**Modo de inteira**:   Sim|  
|**Suprimir a geração de coluna auxiliar ROWID**|Em caso afirmativo, proíbe a criação de criação de auxiliares de coluna ROWD em tabelas de destino. Pode afetar a migração de algumas estruturas.<br /><br />**Modo padrão**:   Não<br /><br />**Modo otimista**:  Não<br /><br />**Modo de inteira**:   Não|  
|**Conversão de instrução TRUNCATE**|Especifica como converter instruções TRUNCATE.<br /><br />**Modo padrão**:   TRUNCATE<br /><br />**Modo otimista**:  TRUNCATE<br /><br />**Modo de inteira**:   TRUNCATE|  
  
### <a name="misc"></a>Diversos  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Mapeamento de esquema padrão**|Especifica como mapear bancos de dados MySQL para esquemas SQL Server.<br /><br />**Modo padrão**:  Banco de dados para o banco de dados<br /><br />**Modo otimista**:  Banco de dados para o banco de dados<br /><br />**Modo de inteira**:  Banco de dados para o banco de dados|  
  
### <a name="procedures-and-functions"></a>Procedimentos e Funções  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Conversão de função padrão**|Especifica se funções deve ser convertido, por padrão para funções T-SQL ou procedimentos armazenados.<br /><br />**Modo padrão**:  Converter em função<br /><br />**Modo otimista**:  Converter em função<br /><br />**Modo de inteira**:  Converter em função|  
|**Gerar SET XACT_ABORT**|Especifica se SET XACT_ABORT ON precisa ser adicionado ao início do procedimento convertido ou gatilho.<br /><br />**Modo padrão**:  Sim<br /><br />**Modo otimista**:  Sim<br /><br />**Modo de inteira**:  Sim|  
|**Gerar SET NOCOUNT em**|Especifica se SET NOCOUNT ON precisa ser adicionado ao início do procedimento convertido ou gatilho.<br /><br />**Modo padrão**:  Sim<br /><br />**Modo otimista**:  Sim<br /><br />**Modo de inteira**:  Sim|  
  
### <a name="spatial-data-types"></a>Tipos de dados espaciais  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Padrão de caixa delimitadora {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} para índices espaciais**|Define o valor padrão para {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} o parâmetro usada em índices espaciais de caixa delimitadora.<br /><br />**Modo padrão**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**Modo otimista**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX:  100<br /><br />YMIN: 0<br /><br />**Modo completo**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0|  
|**Densidade de grade padrão para índices espaciais**|Define o valor padrão para LEVEL_1, LEVEL_2, LEVEL_3 e LEVEL_4 de densidade de grade usada em índices espaciais.<br /><br />**Modo padrão**<br /><br />LEVEL_1: Padrão<br /><br />LEVEL_2: Padrão<br /><br />LEVEL_3: Padrão<br /><br />LEVEL_4: Padrão<br /><br />**Modo otimista**<br /><br />LEVEL_1: Padrão<br /><br />LEVEL_2: Padrão<br /><br />LEVEL_3: Padrão<br /><br />LEVEL_4: Padrão<br /><br />**Modo completo**<br /><br />LEVEL_1: Padrão<br /><br />LEVEL_2: Padrão<br /><br />LEVEL_3: Padrão<br /><br />LEVEL_4: Padrão|  
  
### <a name="transactions"></a>Transações  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Tabelas não transacional**|Especifica se todas as referências à tabela que não dão suporte a transações devem ser marcadas com mensagens de aviso de conversão.<br /><br />**Modo padrão**: Não<br /><br />**Modo otimista**: Não<br /><br />**Modo de inteira**: Sim|  
|**Nível de isolamento da transação**|Especifica o nível de isolamento da transação deve ser usado para novas transações.<br /><br />**Modo padrão**:   Padrão<br /><br />**Modo otimista**:  Padrão<br /><br />**Modo de inteira**:   Leitura repetida|  
  
### <a name="value-control"></a>Controle de valor  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Caractere a conversão numérica**|Especifica como lidar com a conversão implícita e explícita do tipo de dados de caractere para tipos de dados numéricos.<br /><br />**Modo padrão**:   Otimistas<br /><br />**Modo otimista**:  Otimistas<br /><br />**Modo de inteira**:   Preciso|  
|**Controlar valores numéricos não ASSINADOS**|Atribuir valores para parâmetros e variáveis numéricas sem sinal de controle.<br /><br />**Modo padrão**:   Não<br /><br />**Modo otimista**:  Não<br /><br />**Modo de inteira**:   Sim|  
|**Controlar sem sinal de subtração**|Modificar valores negativos inseridos em colunas de tabela do tipo de dados sem sinal.<br /><br />**Modo padrão**:   Converter ' como-está '<br /><br />**Modo otimista**:  Converter ' como-está '<br /><br />**Modo de inteira**:   Marcar com um aviso|  
|**Conversão de e para o tipo de dados binários**|Especifica como lidar com a conversão implícita e explícita do tipo de dados binários.<br /><br />**Modo padrão**:   Otimistas<br /><br />**Modo otimista**:  Otimistas<br /><br />**Modo de inteira**:   Preciso|  
|**Tipo de conversão de dados de data/hora**|Especifica como lidar com a conversão implícita e explícita em data/hora de tipo de dados.<br /><br />**Modo padrão**:   Emular o formato do MySQL<br /><br />**Modo otimista**:  Use o formato do SQL Server<br /><br />**Modo de inteira**:   Emular o formato do MySQL|  
|**Literais numéricos com precisão excedendo 38**|Especifica como converter literais numéricos com precisão excedendo 38.<br /><br />**Modo padrão**:   Se possível de ida e volta<br /><br />**Modo otimista**:  Se possível de ida e volta<br /><br />**Modo de inteira**:   Se possível de ida e volta|  
|**Data de zero em colunas NULL não**|Especifica como lidar com a atribuição não NULL colunas da data de Zero, data de Zero ou valores de data/hora inválido.<br /><br />**Modo padrão**:   GETDATE)<br /><br />**Modo otimista**:  GETDATE)<br /><br />**Modo de inteira**:   GETDATE)|  
  
## <a name="see-also"></a>Consulte também  
[Referência da Interface do usuário &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
  
