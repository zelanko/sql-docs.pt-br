---
title: Definindo opções de Pooling de Conexão de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6a7c21b511f88b8f26d8cc4bdbff40c37c096dcb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="setting-odbc-connection-pooling-options"></a>Definindo opções de Pooling de Conexão de ODBC
O pool de Conexão permite que um aplicativo para usar uma conexão de um pool de conexões que não precisam ser restabelecidas para cada uso. Você pode usar o **Pooling de Conexão** guia do **administrador de fonte de dados ODBC** caixa de diálogo para habilitar e desabilitar o monitoramento do desempenho. Clique duas vezes em um nome de driver para definir o período de tempo limite de conexão.  
  
 No nível do driver, o pooling de conexão é habilitada pelo valor do registro CPTimeout. Este driver de seletivo permite que um administrador do sistema para habilitar o pool de conexão para apenas os drivers que oferecem suporte a ele. Ele é feito definindo o valor padrão de CPTimeout durante o programa de instalação do driver. Clique duas vezes em um nome de driver para definir o período de tempo limite de conexão.  
  
 Para obter mais informações sobre o pool de conexão, consulte [Pooling de Conexão ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Monitoramento de desempenho  
 Monitoramento de desempenho controla o desempenho de conexão por meio do registro de uma variedade de estatísticas. Essas estatísticas podem ser personalizadas pelo desenvolvedor para incluir itens como o seguinte:  
  
|Contador|Definição|  
|-------------|----------------|  
|Contador de disco rígido de Conexão ODBC por segundo|O número de conexões reais por segundo que são feitas no servidor. Na primeira vez em que seu ambiente executa uma carga pesada, esse contador será subir muito rapidamente. Depois de alguns segundos, ele será removido como zero. Isso é a situação normal quando o pooling de conexão está funcionando. Quando as conexões com o servidor foi estabelecidas, eles serão usados e colocados em pool para reutilização.|  
|ODBC rígido desconectar contador por segundo|O número de disco rígido desconexões por segundo emitido para o servidor. Esses são reais conexões com o servidor que estão sendo lançados pelo pool de conexão. Esse valor aumenta de zero quando você interromper todos os clientes no sistema e iniciam as conexões de tempo limite.|  
|Contador de disco de Conexão ODBC por segundo|O número de conexões satisfeitos pelo pool por segundo — em outras palavras, conexões desse pool que foram passadas para os usuários. Este contador indica se o pool está funcionando. Dependendo da carga no servidor, não é incomum para esta opção para mostrar as conexões de software de 40 a 60 por segundo.|  
|Contador de desconexão flexível ODBC por segundo|O número de desconexões por segundo emitido pelos aplicativos. Quando o aplicativo libera ou se desconecta, a conexão é colocado em pool.|  
|Contador de Conexão ativa atual do ODBC|O número de conexões no pool que estão atualmente em uso.|  
|Contador de Conexão livre atual ODBC|O número atual de conexões livres no pool. Essas são as conexões ao vivo que estão disponíveis para uso.|  
|Pools de ativo no momento|O número de pools de ativos no momento. Esse contador foi adicionado no Windows 8, drivers de gerenciam conexões no pool de conexão. Para obter mais informações, consulte [Pooling de Conexão com reconhecimento de Driver](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Pools criados|O número de pools de ativos, incluindo pools ativos e removidos. Esse contador foi adicionado no Windows 8, drivers de gerenciam conexões no pool de conexão. Para obter mais informações, consulte [Pooling de Conexão com reconhecimento de Driver](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 Você deve especificar seus próprios parâmetros de monitoramento. Exemplos de monitoramento de desempenho foram incluídos com esta versão do ODBC.
