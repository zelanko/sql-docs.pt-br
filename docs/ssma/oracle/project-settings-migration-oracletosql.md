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
ms.openlocfilehash: d644a2dd1d8cef03618aec7651b4db37795b1507
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40393341"
---
# <a name="project-settings-migration-oracletosql"></a>Configurações do projeto (migração) (OracleToSQL)
A página de migração do **configurações do projeto** caixa de diálogo contém configurações que personalizam como o SSMA migra dados do Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
O painel de migração está disponível em ambos os **configurações do projeto** e **configurações do projeto padrão** caixas de diálogo.  
  
-   Para especificar configurações para todos os projetos do SSMA, na **ferramentas** menu, selecione **configurações do projeto padrão**, selecione o tipo de projeto de migração para o qual as configurações são necessárias para ser exibida ou alterada de **Versão de destino de migração** suspensa clique **gerais** na parte inferior do painel esquerdo e, em seguida, clique **migração**.  
  
-   Para especificar configurações para o projeto atual, nos **ferramentas** menu, selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e, em seguida, clique em **Migração**.  
  
## <a name="migration-engine"></a>Mecanismo de migração  
  
|Termo|Definição|  
|--------|--------------|  
|**Mecanismo de migração**|Especifica o mecanismo de banco de dados usado durante a migração de dados. Migração de dados do lado cliente refere-se para o cliente SSMA recuperando os dados de origem e de inserção em massa dados em SQL Server. Migração de dados do lado servidor refere-se ao SSMA migração mecanismo de dados (programa de cópia em massa) em execução na caixa de ferramentas do SQL Server como um trabalho do SQL Agent, recuperando dados da origem e inserindo diretamente no SQL Server, evitando, assim, um cliente-salto extra (melhor desempenho).<br /><br />**Modo padrão**: mecanismo de migração de dados do lado cliente<br /><br />**Modo otimista**: mecanismo de migração de dados do lado cliente<br /><br />**Modo de inteira**: mecanismo de migração de dados do lado cliente|  
  
> [!IMPORTANT]  
> Quando o **mecanismo de migração** opção for definida como **mecanismo de migração de dados do lado do servidor**, um novo projeto definindo a opção **o mecanismo de migração de dados do uso de 32 bits servidor lado** é exibido . Especifica se o utilitário de programa de cópia em massa (BCP) de 32 bits ou 64 bits é usado para migrar os dados.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
  
|Termo|Definição|  
|--------|--------------|  
|**Tamanho do lote**|Especifica o lote tamanho usado durante a migração de dados.<br /><br />**Modo padrão**: 10000<br /><br />**Modo otimista**: 10000<br /><br />**Modo de inteira**: 10000|  
|**Verificar restrições**|Especifica se o SSMA deve verificar restrições quando ele insere dados em tabelas do SQL Server.<br /><br />**Modo padrão**: False<br /><br />**Modo otimista**: False<br /><br />**Modo de inteira**: False|  
|**Tempo limite de migração de dados**|Especifica o tempo limite usado durante a migração de dados<br /><br />**Modo padrão**: 15<br /><br />**Modo otimista**: 15<br /><br />**Modo de inteira**: 15|  
|**Opções de migração de dados estendidos**|Mostra as opções de migração de dados extra para cada tabela na guia detalhes separados.<br /><br />**Modo padrão**: ocultar<br /><br />**Modo otimista**: ocultar<br /><br />**Modo de inteira**: ocultar|  
|**Acionadores**|Especifica se o SSMA deve ativar gatilhos de inserção quando ele adiciona dados a tabelas do SQL Server.<br /><br />**Modo padrão**: False<br /><br />**Modo otimista**: False<br /><br />**Modo de inteira**: False|  
|**Manter identidade**|Especifica se o SSMA preserva valores nulos na fonte de dados quando ele adiciona dados ao SQL Server, independentemente dos valores padrão que são especificados no SQL Server.<br /><br />**Modo padrão**: True<br /><br />**Modo otimista**: True<br /><br />**Modo de inteira**: False|  
|**Manter nulos**|Especifica se o SSMA preserva valores nulos na fonte de dados quando ele adiciona dados ao SQL Server, independentemente dos valores padrão que são especificados no SQL Server.<br /><br />**Modo padrão**: True<br /><br />**Modo otimista**: True<br /><br />**Modo de inteira**: True|  
|**Marcar a operação de corte de cadeia de caracteres com erro**|Se o tamanho de coluna de destino é menor que o comprimento da cadeia de caracteres de origem, o valor será cortado e marcado como um erro.<br /><br />**Modo padrão**: Sim<br /><br />**Modo otimista**: Sim<br /><br />**Modo de inteira**: Sim|  
|**Se Houver Erro**|Migração de dados é interrompido quando ocorre um erro. Ele tem três opções:<br /><br />**Interromper a migração:** interrompe a operação de migração de dados<br /><br />**Vá para a tabela a seguir:** interrompe a migração de dados na tabela atual e continua para o próximo<br /><br />**Vá para o próximo lote:** interrompe a migração de dados para o lote atual e continua para o próximo<br /><br />**Modo padrão**: vá para o próximo lote<br /><br />**Modo otimista**: vá para o próximo lote<br /><br />**Modo de inteira**: vá para o próximo lote|  
|**Substituir datas sem suporte**|Especifica se o SSMA deve corrigir as datas anteriores ao mais antigo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** Data (01 de janeiro de 1753).<br /><br />Para manter os valores de data atual, selecione **não fazem nada**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não aceita datas antes de 01 de janeiro de 1753 em uma coluna de data e hora. Se você usar datas mais antigas, você deve converter os valores de data e hora para valores de caractere.<br /><br />Para converter datas antes de 01 de janeiro de 1753 como NULL, selecione **substitua NULL**.<br /><br />Para substituir datas antes de 01 de janeiro de 1753 com uma data com suporte, selecione **substitua mais próximo da data com suporte**.<br /><br />**Modo padrão**: não fazer nada<br /><br />**Modo otimista**: não fazer nada<br /><br />**Modo de inteira**: Substitua mais próximo da data com suporte|  
|**Bloqueio de tabela**|Especifica se o SSMA bloqueia tabelas quando ele adiciona dados às tabelas durante a migração de dados. Obtém um bloqueio de atualização em massa para a duração da operação de cópia em massa. Se o valor for False, um bloqueio é definido no nível de linha.<br /><br />**Modo padrão**: True<br /><br />**Modo otimista**: True<br /><br />**Modo de inteira**: True|  
  
## <a name="parallel-data-migration"></a>Migração de dados em paralelo  
  
|Termo|Definição|  
|--------|--------------|  
|**Modo de migração de dados em paralelo**|Especifica o modo usado para threads de bifurcação para permitir a migração de dados em paralelo. No modo Auto, o SSMA escolhe o número de threads (10 por padrão) bifurcado para migrar os dados. No modo personalizado, o usuário pode especificar o número de threads bifurcado para migrar os dados (o mínimo é 1, e o máximo é 100). Atualmente, somente cliente lado migração mecanismo de dados dá suporte à migração de dados em paralelo.<br /><br />**Modo padrão**: automático<br /><br />**Modo otimista**: automático<br /><br />**Modo de inteira**: automático|  
  
> [!IMPORTANT]  
> Quando o **modo de migração de dados paralelo** opção for definida como **personalizado**, um novo projeto definindo a opção **a contagem de threads** é exibida. Ele especifica o número de threads usados para a migração de dados.  
  
