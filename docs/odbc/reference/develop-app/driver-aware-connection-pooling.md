---
title: Pooling de conexão com reconhecimento de driver | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287596"
---
# <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver
O pool de conexões de reconhecimento de driver é um novo recurso do Driver Manager no Windows 8. O pool de conexões de reconhecimento de driver permite que os escritores de driver personalizem o comportamento de poolde conexão em seu driver ODBC.  
  
> [!NOTE]  
>  O pool de conexões de reconhecimento do driver não é suportado com a biblioteca do cursor. Um aplicativo receberá mensagem de erro se tentar ativar a biblioteca do cursor via SQLSetConnectAttr, quando o pool de conexões de reconhecimento do driver estiver ativado.  
  
 O pool de conexões de reconhecimento de driver aborda os seguintes problemas relacionados ao pool de conexões do Driver Manager:  
  
 **Fragmentação da piscina** O Gerenciador de driver só retornará uma conexão do pool se for uma correspondência exata com a seqüência de conexão de uma nova solicitação de conexão.  Uma das razões para o Driver Manager exigir uma correspondência exata é que o Driver Manager não entende cada palavra-chave de cadeia de conexão específica do driver e seu valor.  No entanto, alguns valores de palavra-chave de seqüência de conexão (como o nome do banco de dados) podem não exigir uma correspondência exata, já que o driver pode alterar o banco de dados em menos do que o tempo necessário para abrir uma nova conexão (a diferença de tempo exata depende da fonte de dados). E, diferenças em alguns atributos de conexão (como SQL_ATTR_CURRENT_CATALOG) podem levar mais tempo para mudar do que diferenças em outros atributos (como SQL_ATTR_LOGIN_TIMEOUT). Isso também pode impedir que o Driver Manager use a conexão reutilizável de menor custo do pool. Quando um driver tem que criar muitas novas conexões, o desempenho de um aplicativo pode diminuir e a escalabilidade da fonte de dados pode diminuir. A fragmentação do pool pode ser reduzida com o pool de conexão com reconhecimento do driver, porque um motorista pode estimar melhor o custo de reutilizar uma conexão no pool para uma solicitação de conexão.  
  
 **Nenhuma consideração da preferência de aplicação** Algumas fontes de dados podem abrir eficientemente novas conexões (em comparação com a redefinição de alguns atributos), então, um aplicativo pode preferir abrir uma nova conexão em vez de tentar reutilizar uma conexão ligeiramente incompatível do pool e redefinir alguns valores (embora isso possa ser mais lento durante a frase de inicialização do pool de conexões). Mas alguns aplicativos podem manter a carga do servidor menor e abrir menos conexões, embora possa haver um custo maior para corrigir as incompatibilidades para o comportamento correto. Sem o pool de conexões com reconhecimento de driver, você não pode especificar esse tipo de preferência efetivamente, porque o Driver Manager não reconhece todos os atributos de conexão específicos do driver. O pool de conexões com reconhecimento de driver permite que um driver obtenha a preferência do usuário (com um atributo específico do driver do SQLSetConnectAttr) para que ele possa estimar melhor o custo de reutilizar uma conexão do pool com base na preferência do usuário.  
  
 Para obter mais informações sobre o pool de conexões com reconhecimento de driver, consulte [O Desenvolvimento da Consciência do Pool de Conexões em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
## <a name="determining-driver-support"></a>Determinando o suporte ao motorista  
 O pool de conexões com reconhecimento de motorista é um recurso opcional que um motorista pode não suportar. Para determinar se um driver o suporta, use o *infoType* SQL_DRIVER_AWARE_POOLING_SUPPORTED do [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
## <a name="how-to-enable-driver-aware-connection-pooling"></a>Como ativar o pool de conexões com reconhecimento de driver  
 Um aplicativo pode usar a consciência de pooling de conexão de um driver definindo o atributo SQL_ATTR_CONNECTION_POOLING para SQL_CP_DRIVER_AWARE com [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). Se um driver não suportar a conscientização do pool de conexões, o pool de conexões driver manager será usado (como se SQL_CP_ONE_PER_HENV tivesse sido especificado, em vez de SQL_CP_DRIVER_AWARE). Os aplicativos ODBC 2.x e 3.x podem habilitar esse recurso.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
