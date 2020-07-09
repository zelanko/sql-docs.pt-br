---
title: MSSQLSERVER_847 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 847 (Database Engine error)
ms.assetid: 67208b7c-bd8d-48a1-9f70-a6488e0f5f9b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d9cf94538afc1614754d72e6b7c8acafdd0f2dbd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727452"
---
# <a name="mssqlserver_847"></a>MSSQLSERVER_847
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|847|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|N/D|  
|Texto da mensagem|Tempo limite esgotado ao aguardar a trava: classe '%ls', id %p, tipo %d, Tarefa 0x%p : %d, tempo de espera %d, sinalizadores 0x%I64x, tarefa proprietária 0x%p. Continuando espera.|  
  
## <a name="explanation"></a>Explicação  
Um computador pode parar de responder ou o fim do tempo limite pode ser alcançado ou outra interrupção das operações regulares pode acontecer ao mesmo tempo em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grava erros de fechamento de buffer no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Se o campo stat na mensagem tiver o valor de 0x04, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está esperando por uma operação de E/S. Você também pode receber a mensagem [MSSQLSERVER_833](~/relational-databases/errors-events/mssqlserver-833-database-engine-error.md) no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Se o campo stat na mensagem não tiver o valor de 0x04, existe grande contenção para uma página. Se o objeto for uma página de dados, isto pode ser causado por um design de código ineficiente. Se a página estiver sem dados, o erro pode ser causado por gargalos de servidor, como recursos de hardware insuficientes.  
  
## <a name="user-action"></a>Ação do usuário  
Para solucionar este problema, dependendo de seu ambiente, o uso de um ou mais dos passos seguintes pode reduzir ou eliminar as mensagens de erro:  
  
-   Determine se você tem algum gargalo de hardware. Se necessário, atualize seu hardware para que ele possa oferecer suporte à configuração, à consulta e aos requisitos de carga de seu ambiente. Para obter mais informações sobre gargalos, consulte [Identify Bottlenecks](~/relational-databases/performance/identify-bottlenecks.md) (Identificar gargalos).  
  
-   Verifique quaisquer erros registrados e execute quaisquer diagnósticos fornecidos por seu fornecedor de hardware.  
  
-   Verifique se suas unidades de disco não estão compactadas. Não há suporte para o armazenamento de dados ou arquivos de log em unidades compactadas. Para obter mais informações sobre arquivos físicos, consulte [Database Files and Filegroups](~/relational-databases/databases/database-files-and-filegroups.md) (Arquivos de banco de dados e grupos de arquivos).  
  
-   Veja se as mensagens de erro desaparecem quando você define as opções a seguir como desativadas:  
  
    -   Opção de configuração de aumento de prioridade do SQL Server  
  
    -   Opção lightweight pooling (modo fibra)  
  
    -   Opção set working set size  
  
    > [!NOTE]  
    > As configurações anteriores frequentemente podem ser contraproducentes se você alterar sua configuração padrão de OFF. Para obter mais informações sobre as configurações, consulte [Server Configuration Options &#40;SQL Server&#41;](~/database-engine/configure-windows/server-configuration-options-sql-server.md) [Opções de configuração do servidor (SQL Server)].  
  
-   Ajuste as consultas para reduzir os recursos usados no sistema. O ajuste do desempenho ajudará a reduzir a tensão em um sistema e melhorar o tempo de resposta para consultas individuais.  
  
-   Defina a opção AUTO_SHRINK como OFF para reduzir a sobrecarga de mudanças para o tamanho do banco de dados.  
  
-   Verifique se você definiu a opção FILEGROWTH para incrementos que sejam grandes o bastante para não serem frequentes. Agende um trabalho para verificar o espaço disponível nos bancos de dados e, depois, aumente o tamanho do banco de dados durante horas fora do pico.  
  
