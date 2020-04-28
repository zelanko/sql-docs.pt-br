---
title: Configurações do projeto (migração) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 40c6c1063ff738428072f3198cae8827e78e2390
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68060156"
---
# <a name="project-settings-migration-db2tosql"></a>Configurações do projeto (migração) (DB2ToSQL)
A página migração da caixa de diálogo **configurações do projeto** contém configurações que personalizam como o SSMA migra dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB2 para o.  
  
O painel migração está disponível nas caixas de diálogo **configurações do projeto** e configurações do **projeto padrão** .  
  
-   Para especificar as configurações para todos os projetos do SSMA, no menu **ferramentas** , selecione **configurações de projeto padrão**, selecione tipo de projeto de migração para o qual as configurações devem ser exibidas ou alteradas na lista suspensa **versão de destino de migração** clique em **geral** na parte inferior do painel esquerdo e clique em **migração**.  
  
-   Para especificar as configurações do projeto atual, no menu **ferramentas** , selecione **configurações do projeto**, clique em **geral** na parte inferior do painel esquerdo e clique em **migração**.  
  
## <a name="migration-engine"></a>Mecanismo de migração  
  
|Termo|Definição|  
|--------|--------------|  
|**Mecanismo de migração**|Especifica o mecanismo de banco de dados usado durante a migração de dado. A migração de dados do lado do cliente refere-se ao cliente do SSMA recuperando os dados da fonte e inserindo esses dados em massa em SQL Server. A migração de dados do lado do servidor refere-se ao mecanismo de migração de dados do SSMA (programa de cópia em massa) em execução na caixa de SQL Server como um trabalho do SQL Agent recuperando dados da origem e inserindo diretamente no SQL Server, evitando assim um salto de cliente extra (melhor desempenho).<br /><br />**Modo padrão**: mecanismo de migração de dados do lado do cliente<br /><br />**Modo otimista**: mecanismo de migração de dados do lado do cliente<br /><br />**Modo completo**: mecanismo de migração de dados do lado do cliente|  
  
> [!IMPORTANT]  
> Quando a opção **mecanismo de migração** é definida como mecanismo de migração de **dados do servidor**, uma nova opção de configuração de projeto usa o **mecanismo de migração de dados do servidor de 32 bits** é exibido. Ele especifica se o utilitário BCP (programa de cópia em massa) de 32 bits ou 64 bits é usado para migrar dados.  
  
## <a name="miscellaneous-options"></a>Opções diversas  
  
|Termo|Definição|  
|--------|--------------|  
|**Tamanho do lote**|Especifica o tamanho do lote usado durante a migração de dados.<br /><br />**Modo padrão**: 10000<br /><br />**Modo otimista**: 10000<br /><br />**Modo completo**: 10000|  
|**Verificar restrições**|Especifica se o SSMA deve verificar as restrições ao inserir dados em SQL Server tabelas.<br /><br />**Modo padrão**: false<br /><br />**Modo otimista**: false<br /><br />**Modo completo**: falso|  
|**Tempo limite de migração de dados**|Especifica o tempo limite usado durante a migração de dados<br /><br />**Modo padrão**: 15<br /><br />**Modo otimista**: 15<br /><br />**Modo completo**: 15|  
|**Opções de migração de dados estendidas**|Mostra opções de migração de dados adicionais para cada tabela na guia detalhes separados.<br /><br />**Modo padrão**: ocultar<br /><br />**Modo otimista**: ocultar<br /><br />**Modo completo**: ocultar|  
|**Acionadores**|Especifica se o SSMA deve acionar gatilhos de inserção ao adicionar dados a tabelas SQL Server.<br /><br />**Modo padrão**: false<br /><br />**Modo otimista**: false<br /><br />**Modo completo**: falso|  
|**Manter identidade**|Especifica se o SSMA preserva valores nulos nos dados de origem quando adiciona dados a SQL Server, independentemente dos valores padrão especificados em SQL Server.<br /><br />**Modo padrão**: verdadeiro<br /><br />**Modo otimista**: verdadeiro<br /><br />**Modo completo**: falso|  
|**Manter nulos**|Especifica se o SSMA preserva valores nulos nos dados de origem quando adiciona dados a SQL Server, independentemente dos valores padrão especificados em SQL Server.<br /><br />**Modo padrão**: verdadeiro<br /><br />**Modo otimista**: verdadeiro<br /><br />**Modo completo**: verdadeiro|  
|**Operação de corte de marca de cadeia de caracteres com erro**|Se o tamanho da coluna de destino for menor que o comprimento da cadeia de caracteres de origem, o valor será cortado e marcado como um erro.<br /><br />**Modo padrão**: Sim<br /><br />**Modo otimista**: Sim<br /><br />**Modo completo**: Sim|  
|**Se houver erro**|Interrompe a migração de dados quando ocorre um erro. Ele tem três opções:<br /><br />**Parar a migração:** Interrompe a operação de migração de dados<br /><br />**Vá para a próxima tabela:** Interrompe a migração de dados para a tabela atual e prossegue para a próxima<br /><br />**Vá para o próximo lote:** Interrompe a migração de dados para o lote atual e prossegue para o próximo<br /><br />**Modo padrão**: Vá para o próximo lote<br /><br />**Modo otimista**: Vá para o próximo lote<br /><br />**Modo completo**: Vá para o próximo lote|  
|**Substituir datas sem suporte**|Especifica se o SSMA deve corrigir datas anteriores à data de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **DateTime** mais antiga (01 de janeiro de 1753).<br /><br />Para manter os valores de data atuais, selecione **não fazer nada**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]não aceitará datas antes de 1º de janeiro de 1753 em uma coluna DateTime. Se você usar datas mais antigas, deverá converter os valores DateTime em valores de caracteres.<br /><br />Para converter datas antes de 1º de janeiro de 1753 a NULL, selecione **substituir por NULL**.<br /><br />Para substituir datas antes de 1º de janeiro de 1753 com uma data com suporte, selecione **substituir pela data com suporte mais próxima**.<br /><br />**Modo padrão**: não fazer nada<br /><br />**Modo otimista**: não fazer nada<br /><br />**Modo completo**: substituir pela data mais próxima com suporte|  
|**Bloqueio de tabela**|Especifica se o SSMA bloqueia as tabelas quando adiciona dados a tabelas durante a migração de dados. Obtém um bloqueio de atualização em massa durante a operação de cópia em massa. Se o valor for false, um bloqueio será definido no nível de linha.<br /><br />**Modo padrão**: verdadeiro<br /><br />**Modo otimista**: verdadeiro<br /><br />**Modo completo**: verdadeiro|  
  
## <a name="parallel-data-migration"></a>Migração de dados paralela  
  
|Termo|Definição|  
|--------|--------------|  
|**Modo de migração de dados paralelos**|Especifica o modo usado para criar o bifurcação de threads para habilitar a migração de dados paralela. No modo auto, o SSMA escolhe o número de threads (10 por padrão) bifurcados para migrar dados. No modo personalizado, o usuário pode especificar o número de threads bifurcados para migrar dados (o mínimo é 1 e o máximo é de 100). Atualmente, somente o mecanismo de migração de dados do lado do cliente dá suporte à migração de dados paralela.<br /><br />**Modo padrão**: automático<br /><br />**Modo otimista**: automático<br /><br />**Modo completo**: automático|  
  
> [!IMPORTANT]  
> Quando a opção **modo de migração de dados paralelo** é definida como **personalizada**, uma nova opção de configuração de projeto **contagem de threads** é exibida. Especifica o número de threads usados para migração de dados.  
  
