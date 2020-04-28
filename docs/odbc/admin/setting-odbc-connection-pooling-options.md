---
title: Definindo opções de pool de conexões ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1d8e66c506518b77320347ce9120254aa1cae287
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307188"
---
# <a name="setting-odbc-connection-pooling-options"></a>Configurar opções de pool de conexões ODBC
O pooling de conexões permite que um aplicativo use uma conexão de um pool de conexões que não precisam ser restabelecidas para cada uso. Você pode usar a guia **pool de conexões** da caixa de diálogo administrador de fonte de **dados ODBC** para habilitar e desabilitar o monitoramento de desempenho. Clique duas vezes em um nome de driver para definir o período de tempo limite de conexão.  
  
 No nível do driver, o pooling de conexão é habilitado pelo valor do registro CPTimeout. Essa habilitação seletiva por driver permite que um administrador do sistema habilite o pool de conexões apenas para os drivers que podem dar suporte a ele. Ela é realizada definindo o valor padrão de CPTimeout durante o programa de instalação do driver. Clique duas vezes em um nome de driver para definir o período de tempo limite de conexão.  
  
 Para obter mais informações sobre o pool de conexões, consulte [ODBC Connection Pooling](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Monitoramento de desempenho  
 O monitoramento de desempenho rastreia o desempenho da conexão gravando uma variedade de estatísticas. Essas estatísticas podem ser personalizadas pelo desenvolvedor para incluir itens como o seguinte:  
  
|Contador|Definição|  
|-------------|----------------|  
|Contador de conexão física ODBC por segundo|O número de conexões reais por segundo que são feitas no servidor. Na primeira vez que o ambiente carrega uma carga pesada, esse contador será atualizado muito rapidamente. Depois de alguns segundos, ele será Descartado para zero. Essa é a situação normal quando o pool de conexões está funcionando. Quando as conexões com o servidor tiverem sido estabelecidas, elas serão usadas e colocadas no pool para reutilização.|  
|Contador de desconexão fixa de ODBC por segundo|O número de desconexões físicas por segundo emitidas para o servidor. Essas são conexões reais com o servidor que estão sendo liberadas pelo pool de conexões. Esse valor aumentará de zero quando você parar todos os clientes no sistema e as conexões começarem a atingir o tempo limite.|  
|Contador de conexões suaves ODBC por segundo|O número de conexões atendidas pelo pool por segundo, em outras palavras, conexões desse pool que foram entregues aos usuários. Este contador indica se o pooling está funcionando. Dependendo da carga no seu servidor, não é incomum que isso mostre 40-60 conexões flexíveis por segundo.|  
|Contador de desconexão de disco ODBC por segundo|O número de desconexões por segundo emitidas pelos aplicativos. Quando o aplicativo libera ou se desconecta, a conexão é colocada de volta no pool.|  
|Contador de conexões ativas ODBC atual|O número de conexões no pool que estão em uso no momento.|  
|Contador de conexão livre atual do ODBC|O número atual de conexões livres disponíveis no pool. Essas são conexões dinâmicas que estão disponíveis para uso.|  
|Pools ativos no momento|O número de pools atualmente ativos. Esse contador foi adicionado ao Windows 8 para drivers que gerenciam conexões no pool de conexões. Para obter mais informações, consulte [pooling de conexão com reconhecimento de driver](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Pools criados|O número de pools ativos, incluindo pools ativos e removidos. Esse contador foi adicionado ao Windows 8 para drivers que gerenciam conexões no pool de conexões. Para obter mais informações, consulte [pooling de conexão com reconhecimento de driver](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 Você deve especificar seus próprios parâmetros de monitoramento. Exemplos de monitoramento de desempenho foram incluídos nesta versão do ODBC.
