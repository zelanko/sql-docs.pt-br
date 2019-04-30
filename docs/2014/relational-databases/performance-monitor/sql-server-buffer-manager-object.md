---
title: SQL Server, objeto Nó de Buffer | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Buffer Manager object
- SQLServer:Buffer Manager
ms.assetid: 9775ebde-111d-476c-9188-b77805f90e98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ed9c8ff90798205f9db02ae4b4b47eb4310d4b06
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250759"
---
# <a name="sql-server-buffer-manager-object"></a>SQL Server, objeto Buffer Manager
  O objeto **Gerenciador de Buffer** fornece contadores para monitorar como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa:  
  
-   Memória para armazenar páginas de dados.  
  
-   Contadores para monitorar a E/S física, como leituras e gravações das páginas do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Extensão do pool de buffers para estender o cache do buffer usando o armazenamento rápido não volátil, como SSD (unidade de estado sólido).  
  
 Monitorar a memória e os contadores usados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ajuda a determinar:  
  
-   Se existem gargalos devidos à memória física inadequada. Caso não consiga armazenar em cache os dados acessados com frequência, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] terá que recuperá-los do disco.  
  
-   Se o desempenho das consultas pode ser melhorado pela adição de memória ou pela disponibilização de mais memória para cache de dados ou para as estruturas internas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   A frequência com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa ler dados a partir do disco. Comparada com outras operações, como acesso de memória, a E/S física demora muito mais. Minimizar a E/S física pode melhorar o desempenho de consulta.  
  
## <a name="buffer-manager-performance-objects"></a>Objetos de desempenho do Gerenciador de Buffer  
 Esta tabela descreve os objetos de desempenho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Gerenciador de Buffer** .  
  
|SQL Server, contadores do Gerenciador de Buffer|Descrição|  
|----------------------------------------|-----------------|  
|**Taxa de acertos do cache do buffer**|Indica a porcentagem de páginas localizadas no cache do buffer sem ter que ler do disco. A taxa é o número total de acertos do cache, dividido pelo número total de pesquisas no cache no acesso dos últimos milhares de páginas. Após um tempo longo, a taxa varia muito pouco. Como ler do cache é muito menos dispendioso que ler do disco, convém que esta taxa seja alta. Geralmente, é possível aumentar a taxa de acertos do cache do buffer aumentando a quantidade de memória disponível para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou usando o recurso de extensão do pool de buffers.|  
|**Páginas de ponto de verificação/s**|Indica o número de páginas liberadas no disco, por segundo, por ponto de verificação ou outra operação que requeira a liberação de todas as páginas sujas.|  
|**Páginas do banco de dados**|Indica o número de páginas no pool de buffers do nó com conteúdo de banco de dados.|  
|**Páginas alocadas pela extensão**|O número total de páginas de cache que não estão livres no arquivo de extensão do pool de buffers.|  
|**Páginas livres de extensão**|O número total de páginas de cache livres no arquivo de extensão do pool de buffers.|  
|**Extensão em uso como porcentagem**|Porcentagem do arquivo de paginação da extensão do pool de buffers ocupada pelas páginas do gerenciador de buffer.|  
|**Contador de E/S pendente de extensão**|Comprimento da fila de E/S para o arquivo de extensão do pool de buffers.|  
|**Remoções da página de extensão/s**|Número de páginas removidas do arquivo de extensão do pool de buffers por segundo.|  
|**Leituras da página de extensão/s**|Número de páginas lidas do arquivo de extensão do pool de buffers por segundo.|  
|**Hora não referenciada da página de extensão**|Média de segundos que uma página ficará na extensão do pool de buffers sem fazer referência a ele.|  
|**Gravações das páginas de extensão/s**|Número de páginas gravadas no arquivo de extensão do pool de buffers por segundo.|  
|**Paradas de lista livre/s**|Indica o número de solicitações, por segundo, que tiveram de esperar por uma página livre.|  
|**Gravações lentas/s**|Indica o número de buffers gravados, por segundo, pelo gravador lento do gerenciador de buffers. O *gravador lento* é um processo do sistema que libera lotes de buffers sujos e velhos (buffers contendo alterações que necessitam de write-back no disco para que o buffer possa ser reutilizado para outra página) e torna-os disponíveis para processos de usuário. O gravador lento elimina a necessidade de executar pontos de verificação frequentes a fim de criar buffers disponíveis.|  
|**Expectativa de vida da página**|Indica o número de segundos que uma página ficará no pool de buffers do nó sem referências.|  
|**Pesquisas de página/s**|Indica o número de solicitações, por segundo, para localizar uma página no pool de buffers.|  
|**Leituras de página/s**|Indica o número de leituras de página de banco de dados física emitidas por segundo. Essa estatística exibe o número total de leituras de página física em todos os bancos de dados. Como a E/S física é dispendiosa, convém minimizar o custo utilizando um maior cache de dados, índices inteligentes e consultas mais eficientes ou alterando o design do banco de dados.|  
|**Gravações de página/s**|Indica o número de gravações de página de banco de dados física emitidas por segundo.|  
|**Páginas lidas por antecipação/s**|Indica o número de páginas lidas, por segundo, antecipadamente ao uso.|  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server:Buffer Node](sql-server-buffer-node.md)   
 [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [SQL Server, objeto Cache de planos](sql-server-plan-cache-object.md)   
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](monitor-resource-usage-system-monitor.md)   
 [sys.dm_os_performance_counters &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql)   
 [Extensão do pool de buffers](../../database-engine/configure-windows/buffer-pool-extension.md)  
  
  
