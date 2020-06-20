---
title: MSSQLSERVER_846 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 846 (Database Engine error)
ms.assetid: ccf367eb-06b0-42b8-b4d6-2b88f4a502d3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6936bcbe6ef59434f0812ac3c25581eb0c1787f0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053633"
---
# <a name="mssqlserver_846"></a>MSSQLSERVER_846
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|846|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|N/D|  
|Texto da mensagem|Tempo limite excedido ao aguardar por fechamento do buffer -- tipo %d, bp %p, página %d:%d, stat %#x, id do banco de dados %d; id da unidade de alocação: %I64d%ls, tarefa 0x%p: %d, tempo de espera %d, sinalizadores 0x%I64x, tarefa proprietária 0x%p. Sem continuação de espera.|  
  
## <a name="explanation"></a>Explicação  
 Um computador pode parar de responder ou o fim do tempo limite pode ser alcançado ou outra interrupção das operações regulares pode acontecer ao mesmo tempo em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grava erros de fechamento de buffer no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o campo stat na mensagem tiver o valor de 0x04, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está esperando por uma operação de E/S. Você também pode receber a mensagem [MSSQLSERVER_833](mssqlserver-833-database-engine-error.md) no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se o campo stat na mensagem não tiver o valor de 0x04, existe grande contenção para uma página. Se o objeto for uma página de dados, isto pode ser causado por um design de código ineficiente. Se a página estiver sem dados, o erro pode ser causado por gargalos de servidor, como recursos de hardware insuficientes.  
  
## <a name="user-action"></a>Ação do usuário  
 Para solucionar este problema, dependendo de seu ambiente, o uso de um ou mais dos passos seguintes pode reduzir ou eliminar as mensagens de erro:  
  
-   Determine se você tem algum gargalo de hardware. Se necessário, atualize seu hardware para que ele possa oferecer suporte à configuração, à consulta e aos requisitos de carga de seu ambiente. Para obter mais informações sobre gargalos, consulte [Identify Bottlenecks](../performance/identify-bottlenecks.md) (Identificar gargalos).  
  
-   Verifique quaisquer erros registrados e execute quaisquer diagnósticos fornecidos por seu fornecedor de hardware.  
  
-   Verifique se suas unidades de disco não estão compactadas. Não há suporte para o armazenamento de dados ou arquivos de log em unidades compactadas. Para obter mais informações sobre arquivos físicos, consulte [Database Files and Filegroups](../databases/database-files-and-filegroups.md) (Arquivos de banco de dados e grupos de arquivos).  
  
-   Veja se as mensagens de erro desaparecem quando você define as opções a seguir como desativadas:  
  
    -   Opção de configuração de aumento de prioridade do SQL Server  
  
    -   Opção lightweight pooling (modo fibra)  
  
    -   Opção set working set size  
  
    > [!NOTE]  
    >  As configurações anteriores frequentemente podem ser contraproducentes se você alterar sua configuração padrão de OFF. Para obter mais informações sobre as configurações, consulte [Server Configuration Options &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md) [Opções de configuração do servidor (SQL Server)].  
  
-   Ajuste as consultas para reduzir os recursos usados no sistema. O ajuste do desempenho ajudará a reduzir a tensão em um sistema e melhorar o tempo de resposta para consultas individuais.  
  
-   Defina a opção AUTO_SHRINK como OFF para reduzir a sobrecarga de mudanças para o tamanho do banco de dados.  
  
-   Verifique se você definiu a opção FILEGROWTH para incrementos que sejam grandes o bastante para não serem frequentes. Agende um trabalho para verificar o espaço disponível nos bancos de dados e, depois, aumente o tamanho do banco de dados durante horas fora do pico.  
  
  
