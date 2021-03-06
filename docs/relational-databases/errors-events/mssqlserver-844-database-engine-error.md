---
description: MSSQLSERVER_844
title: MSSQLSERVER_844 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 844 (Database Engine error)
ms.assetid: 2060c886-1226-4066-bc0c-de90a1cfb82b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1924a8cc064b9c0c7539802b99013ad28d97ce2a
ms.sourcegitcommit: a0245fdae1ff9045f587a3a67b72f34405d35a4f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/19/2020
ms.locfileid: "88618086"
---
# <a name="mssqlserver_844"></a>MSSQLSERVER_844
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|844|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|BUFLATCH_TIMEOUT_CONTINUE|  
|Texto da mensagem|Tempo limite excedido ao aguardar a trava do buffer - tipo %d, bp %p, página %d:%d, stat %#x, id do banco de dados %d; id da unidade de alocação: %I64d%ls, tarefa 0x%p: %d, tempo de espera %d, sinalizadores 0x%I64x, tarefa proprietária 0x%p.  Continuando espera.|  
  
## <a name="explanation"></a>Explicação
Um processo SQL está aguardando travamento. Esse problema pode ser causado por uma operação de E/S que leva muito tempo para ser concluída. Normalmente esse tipo de erro é o resultado de outros processos do sistema de bloqueio de tarefas. Em alguns casos, esse erro pode ser causado por falha de hardware.  Quando essa mensagem de erro ocorre, você pode notar que o computador e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] param de responder.

## <a name="cause"></a>Causa
Essa mensagem de erro depende do ambiente geral do sistema. Qualquer uma das seguintes circunstâncias pode levar a um sistema com sobrecarga:

- Hardware que não atende às suas necessidades de E/S (entrada/saída) e de memória
- Configurações definidas e testadas inadequadamente
- Design ineficiente

 Você pode observar a mensagem de erro 844 quando o sistema está sob uma carga pesada e não é capaz de atender às demandas de carga de trabalho. Algumas das causas mais comuns de um ambiente com sobrecarga são:

- Problemas de hardware
- Volumes compactados
- Definições da configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não padrão
- Consultas ou design de índice ineficientes
- Operações frequentes de crescimento automático ou redução automática de banco de dados

## <a name="user-action"></a>Ação do usuário  
Tente o seguinte para evitar que esse erro ocorra:  
  
- Determine se há algum gargalo de hardware. Confira [Identificando gargalos](../performance/identify-bottlenecks.md) para um bom ponto de partida. Se necessário, atualize o hardware para que ele seja capaz de atender às necessidades de configuração, consultas e carga do seu ambiente.

- Verifique se todo o hardware está funcionando corretamente. Verifique quaisquer erros registrados e execute quaisquer diagnósticos fornecidos por seu fornecedor de hardware. Verifique se há falhas de E/S associadas no log de erros ou no log de eventos. Normalmente as falhas de E/S indicam um funcionamento inadequado do disco.  
- Verifique se seus volumes de disco não estão compactados. Não há suporte para o armazenamento de arquivos de dados e de log em unidades compactadas, confira [Arquivos e grupos de arquivos de banco de dados](../databases/database-files-and-filegroups.md). Para obter informações adicionais sobre o suporte a unidades compactadas, examine o seguinte artigo: [Bancos de dados SQL Server sem suporte em volumes compactados](https://support.microsoft.com/EN-US/help/231347)

- Confira se as mensagens de erro desaparecem quando você desativa as seguintes opções de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:
   - A [opção aumento de prioridade](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)
   - A [opção lightweight pooling (modo fibra)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)
   - A [opção set working set size](../../database-engine/configure-windows/set-working-set-size-server-configuration-option.md)

    Para mais informações, confira [COMO: Determinar as definições de configuração do SQL Server adequadas](https://support.microsoft.com/EN-US/help/319942)

- Ajuste as consultas para reduzir os recursos usados no sistema. O ajuste do desempenho ajudará a reduzir a tensão em um sistema e melhorar o tempo de resposta para consultas individuais.
- Definir a propriedade AutoShrink como OFF para reduzir a sobrecarga de mudanças para o tamanho do banco de dados.
- Verificar se você definiu a propriedade AutoGrow como incrementos que sejam grandes o bastante para não serem frequentes. Agendar um trabalho para verificar o espaço disponível nos bancos de dados e aumentar o tamanho deles durante as horas que não são de pico.
- Verifique no log de erros se existem tarefas não produzidas e outros erros críticos. Resolva esses erros primeiro, pois eles podem apontar para a causa raiz do problema subjacente.
- Caso ocorram erros críticos, como afirmações, com frequência, resolva esses problemas.
- Se as mensagens de erro 844 não forem frequentes, você poderá ignorar os erros.