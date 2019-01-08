---
title: Definindo opções de pool de Conexão de ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15a3efd678d7b1f055daebc31d71d4044ad19eef
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52503892"
---
# <a name="setting-odbc-connection-pooling-options"></a>Configurar opções de pool de conexões ODBC
Pooling de Conexão permite que um aplicativo para usar uma conexão de um pool de conexões que não precisam ser restabelecidas para cada uso. Você pode usar o **Pooling de Conexão** guia da **administrador de fonte de dados ODBC** caixa de diálogo para habilitar e desabilitar o monitoramento de desempenho. Clique duas vezes em um nome de driver para definir o período de tempo limite de conexão.  
  
 Pooling de conexão está habilitada no nível do driver, pelo valor do registro CPTimeout. Este driver de seletivo permite que um administrador do sistema habilitar o pooling de conexão para apenas os drivers que dão suporte a ele. Isso é feito definindo o valor padrão de CPTimeout durante o programa de instalação do driver. Clique duas vezes em um nome de driver para definir o período de tempo limite de conexão.  
  
 Para obter mais informações sobre o pooling de conexão, consulte [Pooling de Conexão ODBC](../../odbc/reference/develop-app/driver-manager-connection-pooling.md).  
  
## <a name="performance-monitoring"></a>Monitoramento de desempenho  
 Monitoramento de desempenho controla o desempenho de conexão por gravar uma variedade de estatísticas. Essas estatísticas podem ser personalizadas pelo desenvolvedor para incluir itens como o seguinte:  
  
|Contador|Definição|  
|-------------|----------------|  
|Contador de disco rígido de Conexão ODBC por segundo|O número de conexões reais por segundo que são feitas no servidor. Na primeira vez em que seu ambiente apresenta uma carga pesada, esse contador será subir muito rapidamente. Depois de alguns segundos, ele descarta a zero. Essa é a situação de normal quando o pooling de conexão está funcionando. Quando as conexões com o servidor tiveram sido estabelecidas, eles serão usados e colocados no pool para reutilização.|  
|ODBC rígido desconectar contador por segundo|O número de disco rígido desconexões por segundo emitido para o servidor. Essas são as conexões reais para o servidor que estão sendo lançadas pelo pool de conexão. Esse valor serão aumentados de zero quando você parar todos os clientes no sistema e as conexões começam a atingir o tempo limite.|  
|Contador de Conexão flexível de ODBC por segundo|O número de conexões satisfeitos por pool por segundo em outras palavras, as conexões do pool que foram entregues aos usuários. Este contador indica se o pool está funcionando. Dependendo da carga em seu servidor, não é incomum para esta opção para mostrar as conexões de software de 40 a 60 por segundo.|  
|Contador de desconexão reversível ODBC por segundo|O número de desconexões por segundo emitido pelos aplicativos. Quando o aplicativo libera ou se desconecta, a conexão é colocado de volta no pool.|  
|Contador de Conexão ativa atual do ODBC|O número de conexões no pool que estão atualmente em uso.|  
|Contador de Conexão livre atual do ODBC|O número atual de conexões livres no pool. Essas são as conexões dinâmicas que estão disponíveis para uso.|  
|Pools de ativo no momento|O número de pools de ativos no momento. Este contador foi adicionado no Windows 8, os drivers que gerenciar conexões no pool de conexão. Para obter mais informações, consulte [Pooling de Conexão de reconhecimento de Driver](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
|Pools criados|O número de pools de Active Directory, incluindo pools do Active Directory e removidos. Este contador foi adicionado no Windows 8, os drivers que gerenciar conexões no pool de conexão. Para obter mais informações, consulte [Pooling de Conexão de reconhecimento de Driver](../../odbc/reference/develop-app/driver-aware-connection-pooling.md).|  
  
 Você deve especificar seus próprios parâmetros de monitoramento. Exemplos para o monitoramento de desempenho foram incluídos com esta versão do ODBC.
