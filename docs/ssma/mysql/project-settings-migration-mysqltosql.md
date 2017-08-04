---
title: "Configurações (migração) (MySQLToSQL) do projeto | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9
caps.latest.revision: 14
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4ab9b6365d527d2cbd804ab0095021c2f2d9dc2b
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="project-settings-migration-mysqltosql"></a>Configurações de projeto (migração) (MySQLToSQL)
A página de migração do **configurações de projeto** caixa de diálogo contém configurações que personalizam como o SSMA migra os dados do MySQL para o SQL Server.  
  
O painel de migração está disponível na **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo.  
  
-   Para especificar configurações para todos os projetos do SSMA, no **ferramentas** menu, selecione **configurações de projeto padrão**, selecione o tipo de projeto no **versão de destino de migração** lista suspensa da qual você deseja acessar as configurações, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **migração**.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu, selecione **configurações de projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **migração**.  
  
## <a name="options"></a>Opções  
  
### <a name="bulk-copy"></a>Cópia em massa  
  
|Termo|Definição|  
|--------|--------------|  
|**Tamanho do lote**|Especifica o lote tamanho usado durante a migração de dados.<br /><br />**Modo padrão**: 1000<br /><br />**Modo otimista**: 1000<br /><br />**Modo de inteira**: 1000|  
|**Verificar restrições**|Especifica se o SSMA deve verificar restrições quando ele insere dados em tabelas do SQL Server.<br /><br />**Modo padrão**: falso<br /><br />**Modo otimista**: falso<br /><br />**Modo de inteira**: falso|  
|**Acionadores**|Especifica se o SSMA deve ativar gatilhos de inserção quando ele adiciona dados a tabelas do SQL Server.<br /><br />**Modo padrão**: falso<br /><br />**Modo otimista**: falso<br /><br />**Modo de inteira**: falso|  
|**Manter identidade**|Especifica se o SSMA preserva valores de identidade do MySQL ao adicionar dados ao SQL Server. Um valor False faz com que valores de identidade seja atribuído pelo destino.<br /><br />**Modo padrão**: True<br /><br />**Modo otimista**: True<br /><br />**Modo de inteira**: True|  
|**Manter nulos**|Especifica se o SSMA preserva valores nulos nos dados de origem ao adicionar dados ao SQL Server, independentemente dos valores padrão que são especificados no SQL Server.<br /><br />**Modo padrão**: True<br /><br />**Modo otimista**: True<br /><br />**Modo de inteira**: True|  
|**Bloqueio de tabela**|Especifica se o SSMA bloqueia tabelas ao adicionar dados às tabelas durante a migração de dados. Obtém um bloqueio de atualização em massa para a duração da operação de cópia em massa. Se o valor for False, um bloqueio é definido no nível de linha.<br /><br />**Modo padrão**: falso<br /><br />**Modo otimista**: falso<br /><br />**Modo de inteira**: falso|  
  
### <a name="data-modification"></a>Modificação de dados  
  
|Termo|Definição|  
|--------|--------------|  
|**Migração de datas inválidas**|Especifica como migrar datas inválidas com como ' 2007-04-23' ou ' 2000-06-31 10:00:00 ' em formatos de data e a data e hora.<br /><br />**Modo padrão**: Definir NULL<br /><br />**Modo otimista**: Definir NULL<br /><br />**Modo de inteira**: Definir NULL|  
|**Valores negativos de tempo migração**|Especifica como migrar valores negativos como '-30:11:00' nas colunas de hora.<br /><br />**Modo padrão**: Definir NULL<br /><br />**Modo otimista**: Definir NULL<br /><br />**Modo de inteira**: Definir NULL|  
|**Valores de hora em 24 horas de migração**|Especifica como migrar os valores de tempo de mais de ' 23: 59:59' nas colunas de hora.<br /><br />**Modo padrão**: Definir NULL<br /><br />**Modo otimista**: Definir NULL<br /><br />**Modo de inteira**: Definir NULL|  
|**Truncar valores binários para caber na coluna**|Em caso afirmativo, o SSMA trunca valores binários do MySQL que não cabem em colunas de tabela do SQL e gera a mensagem de erro apropriada. Se não, a linha faz com que um erro<br /><br />**Modo padrão**: nenhuma<br /><br />**Modo otimista**: nenhuma<br /><br />**Modo de inteira**: nenhuma|  
|**Truncar valores de caractere para caber na coluna**|O SSMA trunca os valores de caractere do MySQL que não cabem em colunas de tabela do SQL e gera a mensagem de erro apropriada.<br /><br />**Modo padrão**: nenhuma<br /><br />**Modo otimista**: nenhuma<br /><br />**Modo de inteira**: nenhuma|  
|**Nenhuma migração de datas**|Especifica como migrar zero datas como ' 0000-00-00' ou ' 0000-00-00-00:00:00 ' nas colunas de data e a data e hora.<br /><br />**Modo padrão**: Definir NULL<br /><br />**Modo otimista**: Definir NULL<br /><br />**Modo de inteira**: Definir NULL|  
|**Zero na migração de datas**|Especifica como migrar datas com zero partes como ' 2009-01-00' ou ' 2000-00-00-11:00:00 ' nas colunas de data e a data e hora.<br /><br />**Modo padrão**: Definir NULL<br /><br />**Modo otimista**: Definir NULL<br /><br />**Modo de inteira**: Definir NULL|  
  
### <a name="migration-engine"></a>Mecanismo de migração  
  
|Termo|Definição|  
|--------|--------------|  
|**Mecanismo de migração**|Especifica o mecanismo de banco de dados usado durante a migração de dados. Migração de dados do lado cliente refere-se ao cliente do SSMA recuperando os dados de origem e em massa inserindo dados no SQL Server. Migração de dados do lado de servidor se refere a SSMA migração mecanismo de dados (programa de cópia em massa) em execução na caixa de ferramentas do SQL Server como um trabalho do SQL Agent, recuperando dados de origem e inserindo diretamente no SQL Server, evitando, assim, um cliente-salto extra (melhor desempenho).<br /><br />**Modo padrão**: mecanismo de migração de dados do lado cliente<br /><br />**Modo otimista**: mecanismo de migração de dados do lado cliente<br /><br />**Modo de inteira**: mecanismo de migração de dados do lado cliente|  
  
> [!IMPORTANT]  
> Quando o **mecanismo de migração** opção é definida como **mecanismo de migração de dados do lado do servidor**, um novo projeto definindo a opção **o mecanismo de migração de dados do uso de 32 bits servidor lado** é exibido. Especifica se o utilitário de programa de cópia em massa (BCP) de 32 bits ou 64 bits é usado para migrar dados.  
  
### <a name="misc"></a>Diversos  
  
|Termo|Definição|  
|--------|--------------|  
|**Opções de migração de dados estendidos**|Mostra as opções de migração de dados extra para cada tabela na guia Detalhes separado.<br /><br />**Modo padrão**: ocultar<br /><br />**Modo otimista**: ocultar<br /><br />**Modo de inteira**: ocultar|  
|**Se Houver Erro**|Migração de dados é interrompido quando ocorre um erro. Ele tem três opções:<br /><br />**Interromper a migração:** interrompe a operação de migração de dados<br /><br />**Vá para a tabela a seguir:** para migração de dados para a tabela atual e passa para o próximo<br /><br />**Vá para o próximo lote:** para migração de dados para o lote atual e passa para o próximo<br /><br />**Modo padrão**: vá para o próximo lote<br /><br />**Modo otimista**: vá para o próximo lote<br /><br />**Modo de inteira**: vá para o próximo lote|  
  
### <a name="parallel-data-migration"></a>Migração de dados em paralelo  
  
|Termo|Definição|  
|--------|--------------|  
|**Modo de migração de dados em paralelo**|Especifica o modo usado para threads de bifurcação para permitir a migração de dados em paralelo. No modo Auto, o SSMA escolhe o número de threads (10 por padrão) bifurcado para migrar os dados. No modo personalizado, o usuário pode especificar o número de threads bifurcada para migrar os dados (o mínimo é 1, e o máximo é 100). No momento, somente cliente lado migração mecanismo de dados oferece suporte à migração de dados em paralelo.<br /><br />**Modo padrão**: automática<br /><br />**Modo otimista**: automática<br /><br />**Modo de inteira**: automática|  
  
> [!IMPORTANT]  
> Quando o **modo de migração de dados paralela** opção é definida como **personalizado**, um novo projeto definindo a opção **a contagem de threads** é exibido. Especifica o número de threads usados para migração de dados.  
  
### <a name="spatial-data"></a>Dados espaciais  
  
|Termo|Definição|  
|--------|--------------|  
|**Tratamento de erros**|Especifica como tratar erros na migração dos valores de tipos de dados espaciais. Se substituir NULL for especificado, todos os valores espaciais causando erros serão substituídos com NULL. Nenhuma substituição é feita caso contrário.<br /><br />**Modo padrão**: gerar um erro<br /><br />**Modo otimista**: gerar um erro<br /><br />**Modo de inteira**: gerar um erro|  
|**Validação do valor**|Especifica como tratar valores espaciais inválidos. Se 'Tente fazer válido' for especificado, está sendo feita uma tentativa para modificar valores inválidos para torná-las válido.<br /><br />**Modo padrão**: tornar válida<br /><br />**Modo otimista**: não altere<br /><br />**Modo de inteira**: tornar válida|  
  

