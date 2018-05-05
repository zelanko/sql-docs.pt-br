---
title: Pooling de Conexão com reconhecimento de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 53e7e3f7-edab-4d0b-8943-45442ba3ebc9
caps.latest.revision: 20
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2efa24f11f174c77ebe7f289019b0544f65d0c2d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver
Pooling de conexão com reconhecimento de driver é um novo recurso do Gerenciador de Driver no Windows 8. Pooling de conexão com reconhecimento de driver permite que os autores de driver personalizar o comportamento no seu driver ODBC de pooling de conexão.  
  
> [!NOTE]  
>  Não há suporte para o pool de conexão com reconhecimento de driver com biblioteca de cursores. Um aplicativo recebe a mensagem de erro ao tentar habilitar a biblioteca de cursores por meio do SQLSetConnectAttr, quando o pooling de conexão com reconhecimento de driver está habilitado.  
  
 Conexão com reconhecimento de driver, o pool de endereços os seguintes problemas relacionados ao pool de conexão do Gerenciador de Driver:  
  
 **Fragmentação do pool** o Gerenciador de Driver retornará apenas uma conexão do pool se for uma correspondência exata com a cadeia de conexão de uma nova solicitação de conexão.  Um motivo para o Gerenciador de Driver para exigir uma correspondência exata é que o Gerenciador de Driver não entender cada palavra-chave de cadeia de caracteres específica do driver de conexão e seu valor.  No entanto, alguns valores de palavra-chave de cadeia de caracteres de conexão (como o nome do banco de dados) podem não exigir uma correspondência exata, pois o driver pode alterar o banco de dados no menor que o tempo necessário para abrir uma nova conexão (a diferença de hora exata depende da fonte de dados). E as diferenças em alguns atributos de conexão (como SQL_ATTR_CURRENT_CATALOG) podem levar mais tempo para alterar de diferenças em outros atributos (como SQL_ATTR_LOGIN_TIMEOUT). Isso, também pode impedir que o Gerenciador de Driver usando a conexão de menor custo, reutilizável do pool. Quando tiver um driver criar várias novas conexões, pode diminuir o desempenho de um aplicativo e a escalabilidade de fonte de dados pode diminuir. Fragmentação do pool pode ser reduzida com o pool de conexão com reconhecimento de driver, porque um driver melhor pode estimar o custo de reutilizar uma conexão no pool para uma solicitação de conexão.  
  
 **Nenhuma consideração de preferência de aplicativo** algumas fontes de dados com eficiência podem abrir novas conexões (comparados à redefinição de alguns atributos), portanto, um aplicativo pode preferir abrir uma nova conexão em vez de tentar reutilizar um pouco incompatíveis conexão do pool e redefinir alguns valores (embora isso possa ser mais lento durante a frase de inicialização do pool de conexão). Mas alguns aplicativos podem manter a carga do servidor menores e abra menos conexões, embora possa haver um custo maior para corrigir as incompatibilidades de comportamento correto. Sem pool de conexão com reconhecimento de driver, você não pode especificar esse tipo de preferência com eficiência, porque o Gerenciador de Driver não reconhece todos os atributos de conexão específicos do driver. Pool de conexão com reconhecimento de driver permite que um driver obter a preferência do usuário (com um atributo específico do driver de SQLSetConnectAttr) para que ele pode melhor estimativa do custo de reutilizar uma conexão do pool com base na preferência do usuário.  
  
 Para obter mais informações sobre o pool de conexão com reconhecimento de driver, consulte [desenvolvendo o reconhecimento do Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Determinando o suporte de Driver  
 Pooling de conexão com reconhecimento de driver é um recurso opcional que não pode dar suporte a um driver. Para determinar se um driver oferece suporte a ele, use o SQL_DRIVER_AWARE_POOLING_SUPPORTED *informação* de [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Como habilitar o pool de Conexão com reconhecimento de Driver  
 Um aplicativo pode usar o reconhecimento de pool de conexão do driver, definindo o atributo SQL_ATTR_CONNECTION_POOLING para SQL_CP_DRIVER_AWARE com [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Se um driver não dá suporte a reconhecimento de pool de conexão, o pool de conexão do Gerenciador de Driver será usado (o mesmo como se tivesse sido especificado SQL_CP_ONE_PER_HENV em vez de SQL_CP_DRIVER_AWARE). Os aplicativos ODBC 2. x e 3. x podem habilitar esse recurso.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
