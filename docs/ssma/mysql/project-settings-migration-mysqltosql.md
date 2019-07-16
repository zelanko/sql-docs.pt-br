---
title: Configurações (migração) (MySQLToSQL) do projeto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2f3c989626f36c003937723869b5e17d1a405ea9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908861"
---
# <a name="project-settings-migration-mysqltosql"></a>Configurações do projeto (migração) (MySQLToSQL)
A página de migração do **configurações do projeto** caixa de diálogo contém configurações que personalizam como o SSMA migra os dados do MySQL para o SQL Server.  
  
O painel de migração está disponível na **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo.  
  
-   Para especificar configurações para todos os projetos do SSMA, na **ferramentas** menu, selecione **configurações do projeto padrão**, selecione o tipo de projeto no **versão de destino de migração** lista suspensa de que você deseja acessar as configurações, clique em **gerais** na parte inferior do painel esquerdo e, em seguida, clique **migração**.  
  
-   Para especificar configurações para o projeto atual, nos **ferramentas** menu, selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **Migração**.  
  
## <a name="options"></a>Opções  
  
### <a name="bulk-copy"></a>Cópia em massa  
  
|Termo|Definição|  
|--------|--------------|  
|**Tamanho do lote**|Especifica o lote tamanho usado durante a migração de dados.<br /><br />**Modo padrão**:  1000<br /><br />**Modo otimista**:  1000<br /><br />**Modo de inteira**:  1000|  
|**Verificar restrições**|Especifica se o SSMA deve verificar restrições quando ele insere dados em tabelas do SQL Server.<br /><br />**Modo padrão**:  False<br /><br />**Modo otimista**:  False<br /><br />**Modo de inteira**:  False|  
|**Acionadores**|Especifica se o SSMA deve ativar gatilhos de inserção quando ele adiciona dados a tabelas do SQL Server.<br /><br />**Modo padrão**:  False<br /><br />**Modo otimista**:  False<br /><br />**Modo de inteira**:  False|  
|**Manter identidade**|Especifica se o SSMA preserva valores de identidade do MySQL quando ele adiciona dados ao SQL Server. Um valor False faz com que os valores de identidade a ser atribuídos pelo destino.<br /><br />**Modo padrão**:  verdadeiro<br /><br />**Modo otimista**:  verdadeiro<br /><br />**Modo de inteira**:  verdadeiro|  
|**Manter nulos**|Especifica se o SSMA preserva valores nulos na fonte de dados quando ele adiciona dados ao SQL Server, independentemente dos valores padrão que são especificados no SQL Server.<br /><br />**Modo padrão**:  verdadeiro<br /><br />**Modo otimista**:  verdadeiro<br /><br />**Modo de inteira**:  verdadeiro|  
|**Bloqueio de tabela**|Especifica se o SSMA bloqueia tabelas quando ele adiciona dados às tabelas durante a migração de dados. Obtém um bloqueio de atualização em massa para a duração da operação de cópia em massa. Se o valor for False, um bloqueio é definido no nível de linha.<br /><br />**Modo padrão**:  False<br /><br />**Modo otimista**:  False<br /><br />**Modo de inteira**:  False|  
  
### <a name="data-modification"></a>Modificação de dados  
  
|Termo|Definição|  
|--------|--------------|  
|**Migração de datas inválidas**|Especifica como a migração de datas inválidas com como ' 2007-04-23' ou ' 2000-06-31 10:00:00 ' nos formatos de data e a data e hora.<br /><br />**Modo padrão**:  Definir nulo<br /><br />**Modo otimista**:  Definir nulo<br /><br />**Modo de inteira**:  Definir nulo|  
|**Valores negativos de tempo migração**|Especifica como migrar valores negativos, como '-30:11:00' nas colunas de tempo.<br /><br />**Modo padrão**:  Definir nulo<br /><br />**Modo otimista**:  Definir nulo<br /><br />**Modo de inteira**:  Definir nulo|  
|**Valores de hora mais de 24 horas de migração**|Especifica como migrar os valores de tempo de mais de ' 23: 59:59' nas colunas de tempo.<br /><br />**Modo padrão**:  Definir nulo<br /><br />**Modo otimista**:  Definir nulo<br /><br />**Modo de inteira**:  Definir nulo|  
|**Truncar valores binários para caber na coluna**|Em caso afirmativo, o SSMA trunca os valores binários do MySQL que não cabem em colunas de tabela do SQL e gera a mensagem de erro apropriada. Se não, a linha causa um erro<br /><br />**Modo padrão**:  Não<br /><br />**Modo otimista**:  Não<br /><br />**Modo de inteira**:  Não|  
|**Truncar os valores de caractere para caber na coluna**|O SSMA trunca os valores de caractere do MySQL que não cabem em colunas de tabela do SQL e gera a mensagem de erro apropriada.<br /><br />**Modo padrão**:  Não<br /><br />**Modo otimista**:  Não<br /><br />**Modo de inteira**:  Não|  
|**Migração zero datas**|Especifica como migrar zero datas como ' 0000-00-00' ou ' 0000-00-00 00:00:00 ' nas colunas de data e a data e hora.<br /><br />**Modo padrão**:  Definir nulo<br /><br />**Modo otimista**:  Definir nulo<br /><br />**Modo de inteira**:  Definir nulo|  
|**Zero na migração de datas**|Especifica como a migração de datas com zero partes, como ' 2009-01-00' ou ' 2000-00-00 11:00:00 ' nas colunas de data e a data e hora.<br /><br />**Modo padrão**:  Definir nulo<br /><br />**Modo otimista**:  Definir nulo<br /><br />**Modo de inteira**:  Definir nulo|  
  
### <a name="migration-engine"></a>Mecanismo de migração  
  
|Termo|Definição|  
|--------|--------------|  
|**Mecanismo de migração**|Especifica o mecanismo de banco de dados usado durante a migração de dados. Migração de dados do lado cliente refere-se para o cliente SSMA recuperando os dados de origem e de inserção em massa dados em SQL Server. Migração de dados do lado servidor refere-se ao SSMA migração mecanismo de dados (programa de cópia em massa) em execução na caixa de ferramentas do SQL Server como um trabalho do SQL Agent, recuperando dados da origem e inserindo diretamente no SQL Server, evitando, assim, um cliente-salto extra (melhor desempenho).<br /><br />**Modo padrão**:  Mecanismo de migração de dados do lado cliente<br /><br />**Modo otimista**:  Mecanismo de migração de dados do lado cliente<br /><br />**Modo de inteira**:  Mecanismo de migração de dados do lado cliente|  
  
> [!IMPORTANT]  
> Quando o **mecanismo de migração** opção for definida como **mecanismo de migração de dados do lado do servidor**, um novo projeto definindo a opção **o mecanismo de migração de dados do uso de 32 bits servidor lado** é exibido . Especifica se o utilitário de programa de cópia em massa (BCP) de 32 bits ou 64 bits é usado para migrar os dados.  
  
### <a name="misc"></a>Diversos  
  
|Termo|Definição|  
|--------|--------------|  
|**Opções de migração de dados estendidos**|Mostra as opções de migração de dados extra para cada tabela na guia detalhes separados.<br /><br />**Modo padrão**:  Ocultar<br /><br />**Modo otimista**:  Ocultar<br /><br />**Modo de inteira**:  Ocultar|  
|**Se Houver Erro**|Migração de dados é interrompido quando ocorre um erro. Ele tem três opções:<br /><br />**Interrompa a migração:** Operação de migração de dados é interrompida<br /><br />**Passe para a tabela a seguir:** Interrompe a migração de dados na tabela atual e continua para o próximo<br /><br />**Vá para o próximo lote:** Interrompe a migração de dados para o lote atual e continua para o próximo<br /><br />**Modo padrão**: Vá para o próximo lote<br /><br />**Modo otimista**: Vá para o próximo lote<br /><br />**Modo de inteira**: Vá para o próximo lote|  
  
### <a name="parallel-data-migration"></a>Migração de dados em paralelo  
  
|Termo|Definição|  
|--------|--------------|  
|**Modo de migração de dados em paralelo**|Especifica o modo usado para threads de bifurcação para permitir a migração de dados em paralelo. No modo Auto, o SSMA escolhe o número de threads (10 por padrão) bifurcado para migrar os dados. No modo personalizado, o usuário pode especificar o número de threads bifurcado para migrar os dados (o mínimo é 1, e o máximo é 100). Atualmente, somente cliente lado migração mecanismo de dados dá suporte à migração de dados em paralelo.<br /><br />**Modo padrão**:  Auto<br /><br />**Modo otimista**:  Auto<br /><br />**Modo de inteira**:  Auto|  
  
> [!IMPORTANT]  
> Quando o **modo de migração de dados paralelo** opção for definida como **personalizado**, um novo projeto definindo a opção **a contagem de threads** é exibida. Ele especifica o número de threads usados para a migração de dados.  
  
### <a name="spatial-data"></a>Dados espaciais  
  
|Termo|Definição|  
|--------|--------------|  
|**Tratando erros**|Especifica como tratar erros na migração de valores de tipos de dados espaciais. Se substituir NULL for especificado, todos os valores espaciais causando erros serão substituídos com NULL. Nenhuma substituição é feita caso contrário.<br /><br />**Modo padrão**:  Gerar um erro<br /><br />**Modo otimista**:  Gerar um erro<br /><br />**Modo de inteira**:  Gerar um erro|  
|**Validação de valor**|Especifica como tratar valores espaciais inválidos. Se 'Tente tornar válido' for especificado, está sendo feita uma tentativa para modificar valores inválidos para torná-los válida.<br /><br />**Modo padrão**: Tornar válida<br /><br />**Modo otimista**: Não alterar<br /><br />**Modo de inteira**: Tornar válida|  
  
