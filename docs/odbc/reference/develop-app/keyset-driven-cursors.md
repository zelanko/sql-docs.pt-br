---
title: Os cursores controlados por conjuntos de chaves | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f908db305a92399ccb5ca9e4930460db249fff46
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="keyset-driven-cursors"></a>Cursores controlados por conjunto de chaves
Um cursor controlado por fica entre static e um cursor dinâmico em sua capacidade de detectar alterações. Como um cursor estático, ele não detectar sempre alterações para a associação e a ordem do conjunto de resultados. Como um cursor dinâmico, ele detectar alterações em valores de linhas no conjunto (sujeito o nível de isolamento da transação, conforme definido pelo atributo de conexão SQL_ATTR_TXN_ISOLATION) de resultados.  
  
 Quando um cursor controlado por conjunto de chaves é aberto, ele salva as chaves para o conjunto de resultados inteiro; Isso corrige a associação aparente e a ordem do conjunto de resultados. Como o cursor percorre o conjunto de resultados, ele usa as chaves na *keyset* para recuperar os valores de dados atual para cada linha. Por exemplo, suponha que um cursor controlado por busca uma linha e outro aplicativo, em seguida, atualiza a linha. Se o cursor refetches a linha, os valores que ele vê são novos, porque ele refetched a linha usando sua chave. Por isso, os cursores controlados por conjuntos de chaves sempre detectam as alterações feitas por si mesmos e outros.  
  
 Quando o cursor tenta recuperar uma linha que foi excluída, essa linha é exibida como um "buraco" no conjunto de resultados: A chave para a linha existe no conjunto de chaves, mas a linha não existe mais no conjunto de resultados. Se os valores de chave em uma linha são atualizados, a linha é considerada foi excluído e, em seguida, inserir, portanto, essas linhas também é exibido como falhas no conjunto de resultados. Enquanto um cursor controlado por conjunto de chaves sempre pode detectar as linhas excluídas por outras pessoas, ele também pode remover as chaves para linhas ela é excluída do conjunto de chaves. Os cursores controlados por conjuntos de chaves que isso não é possível detectar suas próprias exclusões. Se um cursor de cursores controlados por determinado detecta suas próprias exclusões é relatado com a opção SQL_STATIC_SENSITIVITY **SQLGetInfo**.  
  
 Linhas inseridas por outras pessoas nunca são visíveis para um cursor controlado por porque não há chaves para essas linhas existem no conjunto de chaves. No entanto, um cursor controlado por conjunto de chaves pode, opcionalmente, adicionar as chaves para linhas insere em si para o conjunto de chaves. Os cursores controlados por conjuntos de chaves que isso podem detectar suas próprias inserções. Se um cursor de cursores controlados por determinado detecta suas próprias inserções é relatado com a opção SQL_STATIC_SENSITIVITY **SQLGetInfo**.  
  
 A matriz de status de linha especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO ou SQL_ROW_ERROR para qualquer linha. Ele retorna SQL_ROW_UPDATED, SQL_ROW_DELETED ou SQL_ROW_ADDED para linhas que detecta como atualizadas, excluídas ou inseridas.  
  
 Cursores controlados por conjuntos de chaves geralmente são implementados por meio da criação de uma tabela temporária que contém as chaves para cada linha no conjunto de resultados. Porque o cursor também deve determinar se linhas foram atualizadas, esta tabela normalmente contém uma coluna com informações de controle de versão de linha.  
  
 Para rolar sobre o conjunto de resultados original, o cursor controlado por abre um cursor estático sobre a tabela temporária. Para recuperar uma linha no conjunto de resultados original, o cursor primeiro recupera a chave apropriada da tabela temporária e, em seguida, recupera os valores atuais para a linha. Se forem usados cursores em bloco, o cursor deve recuperar várias linhas e chaves.
