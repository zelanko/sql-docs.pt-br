---
title: Configurações (migração) (OracleToSQL) do projeto | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: fcd6b988-633b-4b2b-9f36-6368b5e86b60
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: f5c4568708ddb4b19cd9b49d232746f0b1e7693f
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777812"
---
# <a name="project-settings-migration-oracletosql"></a>Configurações de projeto (migração) (OracleToSQL)
A página de migração do **configurações de projeto** caixa de diálogo contém configurações que personalizam como o SSMA migra os dados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
O painel de migração está disponível em ambos o **configurações de projeto** e **configurações de projeto padrão** caixas de diálogo.  
  
-   Para especificar configurações para todos os projetos do SSMA, no **ferramentas** menu, selecione **configurações de projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibido ou alterado de **versão de destino de migração** suspensa clique **geral** na parte inferior do painel esquerdo e, em seguida, clique **migração**.  
  
-   Para especificar as configurações para o projeto atual, no **ferramentas** menu, selecione **configurações de projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique **migração**.  
  
## <a name="migration-engine"></a>Mecanismo de migração  
  
|Termo|Definição|  
|--------|--------------|  
|**Mecanismo de migração**|Especifica o mecanismo de banco de dados usado durante a migração de dados. Migração de dados do lado cliente refere-se ao cliente do SSMA recuperando os dados de origem e em massa inserindo dados no SQL Server. Migração de dados do lado de servidor se refere a SSMA migração mecanismo de dados (programa de cópia em massa) em execução na caixa de ferramentas do SQL Server como um trabalho do SQL Agent, recuperando dados de origem e inserindo diretamente no SQL Server, evitando, assim, um cliente-salto extra (melhor desempenho).<br /><br />**Modo padrão**: mecanismo de migração de dados do lado cliente<br /><br />**Modo otimista**: mecanismo de migração de dados do lado cliente<br /><br />**Modo de inteira**: mecanismo de migração de dados do lado cliente|  
  
> [!IMPORTANT]  
> Quando o **mecanismo de migração** opção é definida como **mecanismo de migração de dados do lado do servidor**, um novo projeto definindo a opção **o mecanismo de migração de dados do uso de 32 bits servidor lado** é exibido. Especifica se o utilitário de programa de cópia em massa (BCP) de 32 bits ou 64 bits é usado para migrar dados.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
  
|Termo|Definição|  
|--------|--------------|  
|**Tamanho do lote**|Especifica o lote tamanho usado durante a migração de dados.<br /><br />**Modo padrão**: 10000<br /><br />**Modo otimista**: 10000<br /><br />**Modo de inteira**: 10000|  
|**Verificar restrições**|Especifica se o SSMA deve verificar restrições quando ele insere dados em tabelas do SQL Server.<br /><br />**Modo padrão**: falso<br /><br />**Modo otimista**: falso<br /><br />**Modo de inteira**: falso|  
|**Tempo limite de migração de dados**|Especifica o tempo limite usado durante a migração de dados<br /><br />**Modo padrão**: 15<br /><br />**Modo otimista**: 15<br /><br />**Modo de inteira**: 15|  
|**Opções de migração de dados estendidos**|Mostra as opções de migração de dados extra para cada tabela na guia Detalhes separado.<br /><br />**Modo padrão**: ocultar<br /><br />**Modo otimista**: ocultar<br /><br />**Modo de inteira**: ocultar|  
|**Acionadores**|Especifica se o SSMA deve ativar gatilhos de inserção quando ele adiciona dados a tabelas do SQL Server.<br /><br />**Modo padrão**: falso<br /><br />**Modo otimista**: falso<br /><br />**Modo de inteira**: falso|  
|**Manter identidade**|Especifica se o SSMA preserva valores nulos nos dados de origem ao adicionar dados ao SQL Server, independentemente dos valores padrão que são especificados no SQL Server.<br /><br />**Modo padrão**: True<br /><br />**Modo otimista**: True<br /><br />**Modo de inteira**: falso|  
|**Manter nulos**|Especifica se o SSMA preserva valores nulos nos dados de origem ao adicionar dados ao SQL Server, independentemente dos valores padrão que são especificados no SQL Server.<br /><br />**Modo padrão**: True<br /><br />**Modo otimista**: True<br /><br />**Modo de inteira**: True|  
|**Marcar a operação de preparo de cadeia de caracteres com erro**|Se o tamanho de coluna de destino é menor que o comprimento da cadeia de caracteres de origem, o valor será cortado e marcado como um erro.<br /><br />**Modo padrão**: Sim<br /><br />**Modo otimista**: Sim<br /><br />**Modo de inteira**: Sim|  
|**Se Houver Erro**|Migração de dados é interrompido quando ocorre um erro. Ele tem três opções:<br /><br />**Interromper a migração:** interrompe a operação de migração de dados<br /><br />**Vá para a tabela a seguir:** para migração de dados para a tabela atual e passa para o próximo<br /><br />**Vá para o próximo lote:** para migração de dados para o lote atual e passa para o próximo<br /><br />**Modo padrão**: vá para o próximo lote<br /><br />**Modo otimista**: vá para o próximo lote<br /><br />**Modo de inteira**: vá para o próximo lote|  
|**Substitua as datas sem suporte**|Especifica se o SSMA deve corrigir as datas anteriores a primeira [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime** Data (01 de janeiro de 1753).<br /><br />Para manter os valores de data atual, selecione **não fazer nada**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] datas anteriores a 01 de janeiro de 1753 não aceita em uma coluna de data e hora. Se você usar datas mais antigas, você deve converter os valores de data e hora para valores de caractere.<br /><br />Para converter datas anteriores a 01 de janeiro de 1753 como NULL, selecione **substituir com NULL**.<br /><br />Para substituir as datas anteriores a 01 de janeiro de 1753 com uma data com suporte, selecione **substitua mais próximo da data com suporte**.<br /><br />**Modo padrão**: não fazer nada<br /><br />**Modo otimista**: não fazer nada<br /><br />**Modo de inteira**: Substitua mais próximo da data com suporte|  
|**Bloqueio de tabela**|Especifica se o SSMA bloqueia tabelas ao adicionar dados às tabelas durante a migração de dados. Obtém um bloqueio de atualização em massa para a duração da operação de cópia em massa. Se o valor for False, um bloqueio é definido no nível de linha.<br /><br />**Modo padrão**: True<br /><br />**Modo otimista**: True<br /><br />**Modo de inteira**: True|  
  
## <a name="parallel-data-migration"></a>Migração de dados em paralelo  
  
|Termo|Definição|  
|--------|--------------|  
|**Modo de migração de dados em paralelo**|Especifica o modo usado para threads de bifurcação para permitir a migração de dados em paralelo. No modo Auto, o SSMA escolhe o número de threads (10 por padrão) bifurcado para migrar os dados. No modo personalizado, o usuário pode especificar o número de threads bifurcada para migrar os dados (o mínimo é 1, e o máximo é 100). No momento, somente cliente lado migração mecanismo de dados oferece suporte à migração de dados em paralelo.<br /><br />**Modo padrão**: automática<br /><br />**Modo otimista**: automática<br /><br />**Modo de inteira**: automática|  
  
> [!IMPORTANT]  
> Quando o **modo de migração de dados paralela** opção é definida como **personalizado**, um novo projeto definindo a opção **a contagem de threads** é exibido. Especifica o número de threads usados para migração de dados.  
  
