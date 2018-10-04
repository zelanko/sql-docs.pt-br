---
title: Pooling de Conexão de reconhecimento de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8af8085bbbfa793d3bf65836a3efbd0ba68d80f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772306"
---
# <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver
Pooling de conexão com suporte do driver é um novo recurso do Gerenciador de Driver no Windows 8. Pooling de conexão com suporte a driver permite que os gravadores de driver personalizar o comportamento em seu driver ODBC do pooling de conexão.  
  
> [!NOTE]  
>  Pooling de conexão com suporte de driver não é compatível com a biblioteca de cursores. Um aplicativo receberá a mensagem de erro se tentar habilitar a biblioteca de cursores por meio do SQLSetConnectAttr, quando o pooling de conexão com suporte a driver está habilitado.  
  
 Conexão com suporte a driver, o pool de endereços os seguintes problemas relacionados ao pooling de conexão do Gerenciador de Driver:  
  
 **Fragmentação de pool** o Gerenciador de Driver retornará apenas uma conexão do pool se for uma correspondência exata com a cadeia de caracteres de conexão de uma nova solicitação de conexão.  Um motivo para o Gerenciador de Driver para exigir uma correspondência exata é que o Gerenciador de Driver não entende cada palavra-chave de cadeia de conexão específicos de driver e seu valor.  No entanto, alguns valores de palavra-chave de cadeia de caracteres de conexão (como o nome do banco de dados) podem não exigir uma correspondência exata, uma vez que o driver pode alterar o banco de dados em menos do que o tempo necessário para abrir uma nova conexão (a diferença de hora exata depende da fonte de dados). E, as diferenças em alguns atributos de conexão (por exemplo, SQL_ATTR_CURRENT_CATALOG) podem levar mais tempo para mudar do que diferenças nos outros atributos (como SQL_ATTR_LOGIN_TIMEOUT). Isso, também, pode impedir que o Gerenciador de Driver usando a conexão de custo mais baixo e reutilizável do pool. Quando tiver um driver criar várias novas conexões, pode diminuir o desempenho de um aplicativo e a escalabilidade de fonte de dados pode diminuir. Fragmentação do pool pode ser reduzida com o pool de conexão de reconhecimento de driver, porque um driver pode estimar melhor o custo de reutilizar uma conexão no pool para uma solicitação de conexão.  
  
 **Nenhuma consideração de preferência de aplicativo** algumas fontes de dados com eficiência podem abrir novas conexões (em comparação à redefinição de alguns atributos), portanto, um aplicativo talvez prefira abrir uma nova conexão em vez de tentar reutilizar um pouco incompatíveis conexão do pool e redefinir alguns valores (embora isso pode ser mais lento durante a frase de inicialização do pool de conexão). Mas alguns aplicativos podem manter a carga do servidor menores e abra menos conexões, embora possa haver um custo maior para corrigir a incompatibilidade e o comportamento correto. Sem o pooling de conexão de reconhecimento de driver, é possível especificar esse tipo de preferência com eficiência, porque o Gerenciador de Driver não reconhece todos os atributos de conexão específicos de driver. Pooling de conexão de reconhecimento de driver permite que um driver para obter a preferência do usuário (com um atributo específico do driver do SQLSetConnectAttr), de modo que ele pode estimar melhor o custo de reutilizar uma conexão do pool com base na preferência do usuário.  
  
 Para obter mais informações sobre o pooling de conexão de reconhecimento de driver, consulte [desenvolvendo o reconhecimento de Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Determinando o suporte de Driver  
 Pooling de conexão de reconhecimento de driver é um recurso opcional que não pode dar suporte a um driver. Para determinar se um driver dá suporte a ele, use o SQL_DRIVER_AWARE_POOLING_SUPPORTED *tipo de informação* dos [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Como habilitar o Pooling de Conexão de reconhecimento de Driver  
 Um aplicativo pode usar o reconhecimento de pooling de conexão de um driver, definindo o atributo SQL_ATTR_CONNECTION_POOLING como SQL_CP_DRIVER_AWARE com [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Se um driver não oferece suporte a reconhecimento de pool de conexão, pooling de conexão do Gerenciador de Driver será usado (mesmo como se tivesse sido especificado SQL_CP_ONE_PER_HENV em vez de SQL_CP_DRIVER_AWARE). Os aplicativos ODBC 2.x e 3.x podem habilitar esse recurso.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
