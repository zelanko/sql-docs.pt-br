---
title: Pool de conexões com reconhecimento de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b70c841f37bd69179137c807c0dadcfd932d2b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287596"
---
# <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver
O pooling de conexão com reconhecimento de driver é um novo recurso do Gerenciador de driver no Windows 8. O pool de conexões com reconhecimento de driver permite que os gravadores de driver personalizem o comportamento do pool de conexões em seu driver ODBC.  
  
> [!NOTE]  
>  O pool de conexões com reconhecimento de driver não tem suporte com a biblioteca de cursores. Um aplicativo receberá uma mensagem de erro se tentar habilitar a biblioteca de cursor via SQLSetConnectAttr, quando o pooling de conexão com reconhecimento de driver estiver habilitado.  
  
 O pooling de conexão com reconhecimento de driver resolve os seguintes problemas relacionados ao pool de conexões do Gerenciador de driver:  
  
 **Fragmentação do pool** O Gerenciador de driver retornará apenas uma conexão do pool se for uma correspondência exata com a cadeia de conexão de uma nova solicitação de conexão.  Um motivo para o Gerenciador de driver exigir uma correspondência exata é que o Gerenciador de driver não entende cada palavra-chave de cadeia de conexão específica do driver e seu valor.  No entanto, alguns valores de palavra-chave de cadeia de conexão (como o nome do banco de dados) podem não exigir uma correspondência exata, já que o driver pode alterar o banco de dados em menos tempo que o necessário para abrir uma nova conexão (a diferença de tempo exata depende da fonte de dado). E as diferenças em alguns atributos de conexão (como SQL_ATTR_CURRENT_CATALOG) podem levar mais tempo para serem alteradas do que as diferenças em outros atributos (como SQL_ATTR_LOGIN_TIMEOUT). Isso também pode impedir que o Gerenciador de driver use a conexão reutilizável e de menor custo do pool. Quando um driver tem que criar várias novas conexões, o desempenho de um aplicativo pode diminuir e a escalabilidade da fonte de dados pode diminuir. A fragmentação do pool pode ser reduzida com o pool de conexões com suporte a Driver, pois um driver pode estimar melhor o custo da reutilização de uma conexão no pool para uma solicitação de conexão.  
  
 **Nenhuma consideração de preferência do aplicativo** Algumas fontes de dados podem abrir com eficiência novas conexões (em comparação com a redefinição de alguns atributos), portanto, um aplicativo pode preferir abrir uma nova conexão em vez de tentar reutilizar uma conexão ligeiramente incompatível do pool e redefinir alguns valores (embora isso possa ser mais lento durante a frase de inicialização do pool de conexões). Mas alguns aplicativos podem manter a carga do servidor menor e abrir menos conexões, embora possa haver um custo maior para corrigir as incompatibilidades para o comportamento correto. Sem o pool de conexões com reconhecimento de driver, você não pode especificar esse tipo de preferência com eficiência, porque o Gerenciador de driver não reconhece todos os atributos de conexão específicos do driver. O pool de conexões com reconhecimento de driver permite que um driver obtenha a preferência do usuário (com um atributo específico de driver de SQLSetConnectAttr) para que possa estimar melhor o custo de reutilizar uma conexão do pool com base na preferência de um usuário.  
  
 Para obter mais informações sobre o pool de conexões com reconhecimento de driver, consulte [desenvolvendo o reconhecimento do pool de conexões em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Determinando o suporte de driver  
 O pool de conexões com reconhecimento de driver é um recurso opcional que pode não dar suporte a um driver. Para determinar se um driver dá suporte a ele, use o SQL_DRIVER_AWARE_POOLING_SUPPORTED *InfoType* de [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Como habilitar o pool de conexões com reconhecimento de driver  
 Um aplicativo pode usar o reconhecimento de pool de conexões de um driver definindo o atributo SQL_ATTR_CONNECTION_POOLING como SQL_CP_DRIVER_AWARE com [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Se um driver não oferecer suporte ao reconhecimento do pool de conexões, o pool de conexões do Gerenciador de driver será usado (o mesmo que se SQL_CP_ONE_PER_HENV tivesse sido especificado, em vez de SQL_CP_DRIVER_AWARE). Os aplicativos ODBC 2. x e 3. x podem habilitar esse recurso.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
