---
title: Definindo opções de pooling de conexão ODBC | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307188"
---
# <a name="setting-odbc-connection-pooling-options"></a>Configurar opções de pool de conexões ODBC
O pool de conexões permite que um aplicativo use uma conexão a partir de um pool de conexões que não precisam ser restabelecidas para cada uso. Você pode usar a guia **Pooling** de conexões da caixa de diálogo Administrador de origem de **dados ODBC** para ativar e desativar o monitoramento de desempenho. Clique duas vezes em um nome de driver para definir o período de tempo de tempo de conexão.  
  
 No nível do driver, o pool de conexões é habilitado pelo valor do registro CPTimeout. Essa ativação seletiva por driver permite que um administrador do sistema habilite o pool de conexões apenas para os drivers que podem suportar. Ele é realizado definindo o valor padrão do CPTimeout durante o programa de configuração do driver. Clique duas vezes em um nome de driver para definir o período de tempo de tempo de conexão.  
  
 Para obter mais informações sobre pooling de conexões, consulte [Pooling de conexão ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Monitoramento de desempenho  
 O monitoramento de desempenho rastreia o desempenho da conexão registrando uma variedade de estatísticas. Essas estatísticas podem ser personalizadas pelo desenvolvedor para incluir itens como o seguinte:  
  
|Contador|Definição|  
|-------------|----------------|  
|Contador de conexão dura ODBC por segundo|O número de conexões reais por segundo que são feitas ao servidor. A primeira vez que seu ambiente carrega uma carga pesada, este contador vai subir muito rapidamente. Depois de alguns segundos, ele vai cair para zero. Esta é a situação normal quando o pool de conexões está funcionando. Quando as conexões ao servidor forem estabelecidas, elas serão usadas e colocadas no pool para reutilização.|  
|Contador de desconexão dura ODBC por segundo|O número de desconexões duras por segundo emitidas para o servidor. Estas são conexões reais para o servidor que estão sendo liberadas pelo pool de conexões. Esse valor aumentará de zero quando você parar todos os clientes no sistema e as conexões começarem a se essegundo evitar.|  
|Contador de conexão macia ODBC por segundo|O número de conexões satisfeitas pelo pool por segundo, outras palavras, conexões daquele pool que foram entregues aos usuários. Este contador indica se o pooling está funcionando. Dependendo da carga no servidor, não é incomum que isso mostre 40-60 conexões suaves por segundo.|  
|Contador de desconexão macia ODBC por segundo|O número de desconexões por segundo emitidos pelos aplicativos. Quando o aplicativo é liberado ou desconectado, a conexão é colocada de volta no pool.|  
|Contador de conexão ativa atual ODBC|O número de conexões no pool que estão atualmente em uso.|  
|Contador de conexão livre da corrente ODBC|O número atual de conexões gratuitas disponíveis no pool. Estas são conexões ao vivo que estão disponíveis para uso.|  
|Pools atualmente ativos|O número de piscinas atualmente ativa. Este contador foi adicionado no Windows 8, para drivers que gerenciam conexões no pool de conexões. Para obter mais informações, consulte [Pooling de conexão com reconhecimento de driver](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Piscinas criadas|O número de piscinas ativas, incluindo piscinas ativas e removidas. Este contador foi adicionado no Windows 8, para drivers que gerenciam conexões no pool de conexões. Para obter mais informações, consulte [Pooling de conexão com reconhecimento de driver](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 Você deve especificar seus próprios parâmetros de monitoramento. Amostras para monitoramento de desempenho foram incluídas nesta versão do ODBC.
