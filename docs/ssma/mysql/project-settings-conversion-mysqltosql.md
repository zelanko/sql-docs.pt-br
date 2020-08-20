---
description: Configurações do projeto (conversão) (MySQLToSQL)
title: Configurações do projeto (conversão) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 7ad5fe44-6445-4ba8-a457-5af792631f11
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 4c2c4c093fec21723584538dfb5585a74e15c8fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492429"
---
# <a name="project-settings-conversion-mysqltosql"></a>Configurações do projeto (conversão) (MySQLToSQL)
A página conversão da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA converte a sintaxe do MySQL em sintaxe SQL Server ou SQL Azure.  
  
O painel de conversão está disponível nas caixas de diálogo **configurações do projeto** e **configurações do projeto padrão** .  
  
-   Use a caixa de diálogo **configurações de projeto padrão** para definir opções de configuração para todos os projetos. Para acessar as configurações de conversão, no menu **ferramentas** , selecione **configurações de projeto padrão**, selecione tipo de projeto de migração para o qual as configurações devem ser exibidas/Changed do menu suspenso **versão de destino de migração** , clique em **geral** na parte inferior do painel esquerdo e, em seguida, selecione **conversão**.  
  
-   Para especificar as configurações para o projeto atual, no menu **ferramentas** , clique em **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **conversão**.  
  
## <a name="options"></a>Opções  
  
### <a name="collate-clause"></a>Cláusula COLLATE  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Conversão de cláusula COLLATE explícita**|A opção de conversão de cláusula COLLATE explícita especifica como converter cláusulas de agrupamento explícitas no código MySQL. Opções possíveis: ignorar e marcar com um aviso/gerar um erro<br /><br />**Modo padrão**: ignorar e marcar com um aviso<br /><br />**Modo otimista**: ignorar e marcar com um aviso<br /><br />**Modo completo**: ignorar e marcar com um aviso|  
  
### <a name="column-constraints"></a>Restrições de coluna  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Gerar restrição para colunas de tipo de dados ENUM**|Gera restrição para colunas de tipo de dados ENUM na tabela SQL Server ou SQL Azure, se não estiver presente na tabela MySQL. Em caso afirmativo, todas as colunas convertidas do tipo de dados ENUM serão acompanhadas com a restrição CHECK que controla o valor.<br /><br />**Modo padrão**: não<br /><br />**Modo otimista**: não<br /><br />**Modo completo**: Sim|  
|**Gerar restrição para colunas do tipo de dados SET**|Gera restrição para colunas do tipo de dados SET na tabela SQL Server ou SQL Azure, se não estiver presente na tabela MySQL. Em caso afirmativo, todas as colunas convertidas do tipo de dados SET serão acompanhadas com a restrição CHECK que controla o valor.<br /><br />**Modo padrão**: não<br /><br />**Modo otimista**: não<br /><br />**Modo completo**: Sim|  
|**Gerar restrição para colunas de colunas de tipo de dados numéricos não assinados**|Adicione verificação de valor não negativo a colunas de tipos de dados numéricos não ASSINADOs.<br /><br />**Modo padrão**: não<br /><br />**Modo otimista**: não<br /><br />**Modo completo**: Sim|  
|**Gerar restrição para colunas de tipo de dados YEAR**|Gera a restrição para colunas de tipo de dados YEAR na tabela SQL Server ou SQL Azure, se ela não estiver presente na tabela MySQL. Em caso afirmativo, todas as colunas convertidas do tipo de dados YEAR serão acompanhadas com a restrição CHECK que controla o valor.<br /><br />**Modo padrão**: não<br /><br />**Modo otimista**: não<br /><br />**Modo completo**: Sim|  
  
### <a name="data-types"></a>Tipos de dados  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Conversão de tipo de dados de enumeração**|Especifica como o tipo de dados ENUM do MySQL deve ser convertido como convertido em NVARCHAR ou converter em numeric<br /><br />**Modo padrão**: converter em nvarchar<br /><br />**Modo otimista**: converter em nvarchar<br /><br />**Modo completo**: converter em nvarchar|  
|**DEFINIR conversão de tipo de dados**|Especifica como o tipo de dados SET do MySQL deve ser convertido, convertido em NVARCHAR (L)/Convert em BINARY (L)<br /><br />**Modo padrão**: converter em nvarchar (L)<br /><br />**Modo otimista**: converter em nvarchar (L)<br /><br />**Modo completo**: converter em nvarchar (L)|  
  
### <a name="generic"></a>Genérico  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Colunas sem o valor padrão em inserir e substituir**|Se ' Yes ', todas as instruções que fazem referência a tabelas usando mecanismos armazenados diferentes de MyISAM e InnoDb devem ser marcadas com mensagens de conversão de aviso.<br /><br />**Modo padrão**: adicionar à lista de colunas<br /><br />**Modo otimista**: adicionar à lista de colunas<br /><br />**Modo completo**: adicionar à lista de colunas|  
|**A conversão de divisão por zero produz**|Especifica se deseja ou não emular o MySQL sem comportamento ERROR_FOR_DIVISION_BY_ZERO.<br /><br />**Modo padrão**: erro<br /><br />**Modo otimista**: erro<br /><br />**Modo completo**: nulo|  
|**Operador IN**|Especifica como converter o MySQL em operador.<br /><br />**Modo padrão**: sempre converter em em<br /><br />**Modo otimista**: sempre converter em em<br /><br />**Modo completo**: expanda se necessário|  
|**Conversão de função MySQL**|Especifica como converter as funções padrão do MySQL.<br /><br />**Modo padrão**: otimista<br /><br />**Modo otimista**: otimista<br /><br />**Modo completo**: preciso|  
|**Mecanismos de armazenamento sem suporte**|Se ' Yes ', todas as instruções que fazem referência a tabelas usando mecanismos armazenados diferentes de MyISAM e InnoDb devem ser marcadas com mensagens de conversão de aviso.<br /><br />**Modo padrão**: não<br /><br />**Modo otimista**: não<br /><br />**Modo completo**: Sim|  
|**Suprimir geração de coluna auxiliar de ROWID**|Em caso afirmativo, proíbe a criação da criação de coluna auxiliar ROWD em tabelas de destino. Pode afetar a migração de algumas estruturas.<br /><br />**Modo padrão**: não<br /><br />**Modo otimista**: não<br /><br />**Modo completo**: não|  
|**TRUNCAr conversão de instrução**|Especifica como converter as instruções de TRUNCAmento.<br /><br />**Modo padrão**: truncar<br /><br />**Modo otimista**: truncar<br /><br />**Modo completo**: truncar|  
  
### <a name="misc"></a>Diversos  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Mapeamento de esquema padrão**|Especifica como mapear bancos de dados MySQL em esquemas de SQL Server.<br /><br />**Modo padrão**: banco de dados para banco de dados<br /><br />**Modo otimista**: banco de dados para banco de dados<br /><br />**Modo completo**: banco de dados para banco de dados|  
  
### <a name="procedures-and-functions"></a>Procedimentos e Funções  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Conversão de função padrão**|Especifica se as funções devem ser, por padrão, convertidas em funções T-SQL ou em procedimentos armazenados.<br /><br />**Modo padrão**: converter em função<br /><br />**Modo otimista**: converter em função<br /><br />**Modo completo**: converter em função|  
|**Gerar conjunto de XACT_ABORT em**|Especifica se o conjunto de XACT_ABORT deve ser adicionado ou não ao início do procedimento ou gatilho convertido.<br /><br />**Modo padrão**: Sim<br /><br />**Modo otimista**: Sim<br /><br />**Modo completo**: Sim|  
|**Gerar definir NOCOUNT em**|Especifica se a definição de NOCOUNT ON precisa ser adicionada ao início do procedimento ou gatilho convertido.<br /><br />**Modo padrão**: Sim<br /><br />**Modo otimista**: Sim<br /><br />**Modo completo**: Sim|  
  
### <a name="spatial-data-types"></a>Tipos de dados espaciais  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Caixa delimitadora padrão {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} para índices espaciais**|Define o valor padrão para o parâmetro {XMAX&#124;XMIN&#124;YMAX&#124;YMIN} da caixa delimitadora usada em índices espaciais.<br /><br />**Modo Padrão**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**Modo otimista**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0<br /><br />**Modo completo**<br /><br />XMAX: 100<br /><br />XMIN: 0<br /><br />YMAX: 100<br /><br />YMIN: 0|  
|**Densidade de grade padrão para índices espaciais**|Define o valor padrão para LEVEL_1, LEVEL_2, LEVEL_3 e LEVEL_4 da densidade de grade usada em índices espaciais.<br /><br />**Modo Padrão**<br /><br />LEVEL_1: padrão<br /><br />LEVEL_2: padrão<br /><br />LEVEL_3: padrão<br /><br />LEVEL_4: padrão<br /><br />**Modo otimista**<br /><br />LEVEL_1: padrão<br /><br />LEVEL_2: padrão<br /><br />LEVEL_3: padrão<br /><br />LEVEL_4: padrão<br /><br />**Modo completo**<br /><br />LEVEL_1: padrão<br /><br />LEVEL_2: padrão<br /><br />LEVEL_3: padrão<br /><br />LEVEL_4: padrão|  
  
### <a name="transactions"></a>Transactions  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Tabelas não transacionais**|Especifica se todas as referências à tabela que não dão suporte a transações devem ser marcadas com mensagens de conversão de aviso.<br /><br />**Modo padrão**: não<br /><br />**Modo otimista**: não<br /><br />**Modo completo**: Sim|  
|**Nível de isolamento da transação**|Especifica qual nível de isolamento da transação deve ser usado para novas transações.<br /><br />**Modo padrão**: padrão<br /><br />**Modo otimista**: padrão<br /><br />**Modo completo**: leitura repetida|  
  
### <a name="value-control"></a>Controle de valor  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Conversão de caractere em numérico**|Especifica como tratar a conversão implícita e explícita do tipo de dados character para tipos de dados numéricos.<br /><br />**Modo padrão**: otimista<br /><br />**Modo otimista**: otimista<br /><br />**Modo completo**: preciso|  
|**Controlar valores numéricos não assinados**|Controle atribuindo valores a variáveis numéricas e parâmetros não assinados.<br /><br />**Modo padrão**: não<br /><br />**Modo otimista**: não<br /><br />**Modo completo**: Sim|  
|**Controlar a subtração não assinada**|Modificar valores negativos inseridos em colunas de tabela de tipo de dados não assinado.<br /><br />**Modo padrão**: converter ' as-is '<br /><br />**Modo otimista**: converter ' as-is '<br /><br />**Modo completo**: marcar com um aviso|  
|**Conversão de e para tipo de dados Binary**|Especifica como tratar a conversão implícita e explícita do tipo de dados Binary.<br /><br />**Modo padrão**: otimista<br /><br />**Modo otimista**: otimista<br /><br />**Modo completo**: preciso|  
|**Conversão para tipo de dados de data/hora**|Especifica como tratar a conversão implícita e explícita para o tipo de dados de data/hora.<br /><br />**Modo padrão**: emular formato MySQL<br /><br />**Modo otimista**: usar formato de SQL Server<br /><br />**Modo completo**: emular formato MySQL|  
|**Literais numéricos com precisão excedendo 38**|Especifica como converter literais numéricos com precisão que excede 38.<br /><br />**Modo padrão**: arredondar se possível<br /><br />**Modo otimista**: arredondar se possível<br /><br />**Modo completo**: arredondar se possível|  
|**Zero-data em colunas não nulas**|Especifica como tratar a atribuição para colunas não nulas de valores de data/hora zeros, zero-in-Date ou inválidos.<br /><br />**Modo padrão**: GETDATE ()<br /><br />**Modo otimista**: GETDATE ()<br /><br />**Modo completo**: GETDATE ()|  
  
## <a name="see-also"></a>Consulte Também  
[Referência da interface do usuário &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
  
