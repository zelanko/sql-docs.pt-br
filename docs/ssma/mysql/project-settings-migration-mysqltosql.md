---
title: Configurações do projeto (migração) (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: fe0c1ac52a72a627cf6b266fdb9636878be85c1a
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935195"
---
# <a name="project-settings-migration-mysqltosql"></a>Configurações do projeto (migração) (MySQLToSQL)
A página migração da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA migra dados do MySQL para o SQL Server.  
  
O painel migração está disponível nas caixas de diálogo **configurações do projeto** e **configurações padrão do projeto** .  
  
-   Para especificar as configurações para todos os projetos do SSMA, no menu **ferramentas** , selecione **configurações de projeto padrão**, selecione o tipo de projeto na lista de **versão de destino de migração** da qual você deseja acessar as configurações, clique em **geral** na parte inferior do painel esquerdo e clique em **migração**.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e clique em **migração**.  
  
## <a name="options"></a>Opções  
  
### <a name="bulk-copy"></a>Cópia em massa  
  
|Termo|Definição|  
|--------|--------------|  
|**Tamanho do lote**|Especifica o tamanho do lote usado durante a migração de dados.<br /><br />**Modo padrão**: 1000<br /><br />**Modo otimista**: 1000<br /><br />**Modo completo**: 1000|  
|**Verificar restrições**|Especifica se o SSMA deve verificar as restrições ao inserir dados em SQL Server tabelas.<br /><br />**Modo padrão**: false<br /><br />**Modo otimista**: false<br /><br />**Modo completo**: falso|  
|**Acionadores**|Especifica se o SSMA deve acionar gatilhos de inserção ao adicionar dados a tabelas SQL Server.<br /><br />**Modo padrão**: false<br /><br />**Modo otimista**: false<br /><br />**Modo completo**: falso|  
|**Manter identidade**|Especifica se o SSMA preserva os valores de identidade do MySQL ao adicionar dados a SQL Server. Um valor de false faz com que os valores de identidade sejam atribuídos pelo destino.<br /><br />**Modo padrão**: verdadeiro<br /><br />**Modo otimista**: verdadeiro<br /><br />**Modo completo**: verdadeiro|  
|**Manter nulos**|Especifica se o SSMA preserva valores nulos nos dados de origem quando adiciona dados a SQL Server, independentemente dos valores padrão especificados em SQL Server.<br /><br />**Modo padrão**: verdadeiro<br /><br />**Modo otimista**: verdadeiro<br /><br />**Modo completo**: verdadeiro|  
|**Bloqueio de tabela**|Especifica se o SSMA bloqueia as tabelas quando adiciona dados a tabelas durante a migração de dados. Obtém um bloqueio de atualização em massa durante a operação de cópia em massa. Se o valor for false, um bloqueio será definido no nível de linha.<br /><br />**Modo padrão**: false<br /><br />**Modo otimista**: false<br /><br />**Modo completo**: falso|  
  
### <a name="data-modification"></a>Modificação de dados  
  
|Termo|Definição|  
|--------|--------------|  
|**Migração de datas inválida**|Especifica como migrar datas inválidas como ' 2007-04-23 ' ou ' 2000-06-31 10:00:00 ' nos formatos de data e DATETIME.<br /><br />**Modo padrão**: definir nulo<br /><br />**Modo otimista**: definir nulo<br /><br />**Modo completo**: definir nulo|  
|**Migração de valores de tempo negativos**|Especifica como migrar valores negativos como '-30:11:00 ' em colunas de tempo.<br /><br />**Modo padrão**: definir nulo<br /><br />**Modo otimista**: definir nulo<br /><br />**Modo completo**: definir nulo|  
|**Valores de tempo em migração de 24 horas**|Especifica como migrar valores de tempo de mais de ' 23:59:59 ' em colunas de tempo.<br /><br />**Modo padrão**: definir nulo<br /><br />**Modo otimista**: definir nulo<br /><br />**Modo completo**: definir nulo|  
|**Truncar valores binários para ajustar à coluna**|Se sim, o SSMA trunca os valores binários do MySQL que não se ajustam às colunas da tabela SQL e gera a mensagem de erro apropriada. Se não, a linha causará um erro<br /><br />**Modo padrão**: não<br /><br />**Modo otimista**: não<br /><br />**Modo completo**: não|  
|**Truncar valores de caracteres para caber na coluna**|O SSMA trunca os valores de caracteres do MySQL que não se ajustam às colunas da tabela SQL e gera a mensagem de erro apropriada.<br /><br />**Modo padrão**: não<br /><br />**Modo otimista**: não<br /><br />**Modo completo**: não|  
|**Migração de datas zero**|Especifica como migrar datas zero como ' 0000-00-00 ' ou ' 0000-00-00 00:00:00 ' nas colunas DATE e DATETIME.<br /><br />**Modo padrão**: definir nulo<br /><br />**Modo otimista**: definir nulo<br /><br />**Modo completo**: definir nulo|  
|**Zero na migração de datas**|Especifica como migrar datas com partes zero, como ' 2009-01-00 ' ou ' 2000-00-00 11:00:00 ', nas colunas DATE e DATETIME.<br /><br />**Modo padrão**: definir nulo<br /><br />**Modo otimista**: definir nulo<br /><br />**Modo completo**: definir nulo|  
  
### <a name="migration-engine"></a>Mecanismo de migração  
  
|Termo|Definição|  
|--------|--------------|  
|**Mecanismo de migração**|Especifica o mecanismo de banco de dados usado durante a migração de dado. A migração de dados do lado do cliente refere-se ao cliente do SSMA recuperando os dados da fonte e inserindo esses dados em massa em SQL Server. A migração de dados do lado do servidor refere-se ao mecanismo de migração de dados do SSMA (programa de cópia em massa) em execução na caixa de SQL Server como um trabalho do SQL Agent recuperando dados da origem e inserindo diretamente no SQL Server, evitando assim um salto de cliente extra (melhor desempenho).<br /><br />**Modo padrão**: mecanismo de migração de dados do lado do cliente<br /><br />**Modo otimista**: mecanismo de migração de dados do lado do cliente<br /><br />**Modo completo**: mecanismo de migração de dados do lado do cliente|  
  
> [!IMPORTANT]  
> Quando a opção **mecanismo de migração** é definida como mecanismo de migração de **dados do servidor**, uma nova opção de configuração de projeto usa o **mecanismo de migração de dados do servidor de 32 bits** é exibido. Ele especifica se o utilitário BCP (programa de cópia em massa) de 32 bits ou 64 bits é usado para migrar dados.  
  
### <a name="misc"></a>Diversos  
  
|Termo|Definição|  
|--------|--------------|  
|**Opções de migração de dados estendidas**|Mostra opções de migração de dados adicionais para cada tabela na guia detalhes separados.<br /><br />**Modo padrão**: ocultar<br /><br />**Modo otimista**: ocultar<br /><br />**Modo completo**: ocultar|  
|**Se houver erro**|Interrompe a migração de dados quando ocorre um erro. Ele tem três opções:<br /><br />**Parar a migração:** Interrompe a operação de migração de dados<br /><br />**Vá para a próxima tabela:** Interrompe a migração de dados para a tabela atual e prossegue para a próxima<br /><br />**Vá para o próximo lote:** Interrompe a migração de dados para o lote atual e prossegue para o próximo<br /><br />**Modo padrão**: Vá para o próximo lote<br /><br />**Modo otimista**: Vá para o próximo lote<br /><br />**Modo completo**: Vá para o próximo lote|  
  
### <a name="parallel-data-migration"></a>Migração de dados paralela  
  
|Termo|Definição|  
|--------|--------------|  
|**Modo de migração de dados paralelos**|Especifica o modo usado para criar o bifurcação de threads para habilitar a migração de dados paralela. No modo auto, o SSMA escolhe o número de threads (10 por padrão) bifurcados para migrar dados. No modo personalizado, o usuário pode especificar o número de threads bifurcados para migrar dados (o mínimo é 1 e o máximo é de 100). Atualmente, somente o mecanismo de migração de dados do lado do cliente dá suporte à migração de dados paralela.<br /><br />**Modo padrão**: automático<br /><br />**Modo otimista**: automático<br /><br />**Modo completo**: automático|  
  
> [!IMPORTANT]  
> Quando a opção **modo de migração de dados paralelo** é definida como **personalizada**, uma nova opção de configuração de projeto **contagem de threads** é exibida. Especifica o número de threads usados para migração de dados.  
  
### <a name="spatial-data"></a>Dados espaciais  
  
|Termo|Definição|  
|--------|--------------|  
|**Tratando erros**|Especifica como tratar erros na migração de valores de tipos de dados espaciais. Se ' Replace with NULL ' for especificado, todos os valores espaciais que causam erros serão substituídos por NULL. Nenhuma substituição é feita de outra forma.<br /><br />**Modo padrão**: gerar um erro<br /><br />**Modo otimista**: gerar um erro<br /><br />**Modo completo**: gerar um erro|  
|**Validação de valor**|Especifica como tratar valores espaciais inválidos. Se ' Try Make válido ' for especificado, será feita uma tentativa de modificar valores inválidos para torná-los válidos.<br /><br />**Modo padrão**: tornar válido<br /><br />**Modo otimista**: não alterar<br /><br />**Modo completo**: tornar válido|  
  
