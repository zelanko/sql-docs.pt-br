---
title: Cursores controlados por | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- keyset-driven cursors [ODBC]
- cursors [ODBC], key-set driven
ms.assetid: 01769f43-1d9c-4685-84fa-15a6465335e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be6dc5a164220befb534368eace4f51f4dbd84e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213443"
---
# <a name="keyset-driven-cursors"></a>Cursores controlados por conjunto de chaves
Um cursor controlado por conjunto de chaves se encontra entre um estático e um cursor dinâmico em sua capacidade de detectar alterações. Como um cursor estático, ele nem sempre detecta alterações à associação e à ordem do conjunto de resultados. Como um cursor dinâmico, ele detectar alterações nos valores de linhas no resultado definido (sujeito ao nível de isolamento da transação, conforme definido pelo atributo SQL_ATTR_TXN_ISOLATION conexão).  
  
 Quando um cursor controlado por conjunto de chaves é aberto, ele salva as chaves para o conjunto de resultados inteiro; Isso corrige a associação aparente e a ordem do conjunto de resultados. Como o cursor percorre o conjunto de resultados, ele usa as chaves desta *keyset* para recuperar os valores de dados atual para cada linha. Por exemplo, suponha que um cursor controlado por busca uma linha e o outro aplicativo, em seguida, atualiza a linha. Se o cursor refetches a linha, os valores que ele vê são novos, porque ele refetched usando sua chave de linha. Por isso, os cursores controlados por sempre detectam as alterações feitas por si só e outras pessoas.  
  
 Quando o cursor tenta recuperar uma linha que foi excluída, essa linha é exibida como uma "brecha" no conjunto de resultados: A chave para a linha existe no conjunto de chaves, mas a linha não existe mais no conjunto de resultados. Se os valores de chave em uma linha forem atualizados, a linha é considerada foi excluído e, em seguida, inserida, para que essas linhas também aparecem como brechas no conjunto de resultados. Enquanto um cursor controlado por sempre pode detectar linhas excluídas por outras pessoas, ele pode, opcionalmente, remover as chaves para linhas ele exclui em si do conjunto de chaves. Cursores controlados por que isso não é possível detectar suas próprias exclusões. Se um cursor específico de cursores controlados por detecta suas própria exclusões é relatado por meio da opção SQL_STATIC_SENSITIVITY na **SQLGetInfo**.  
  
 Linhas inseridas por outras pessoas nunca são visíveis para um cursor controlado por porque nenhuma chave para essas linhas existe no conjunto de chaves. No entanto, um cursor controlado por conjunto de chaves, opcionalmente, pode adicionar as chaves para linhas insere em si para o conjunto de chaves. Os cursores controlados por fazem isso podem detectar suas próprias inserções. Se um cursor específico de cursores controlados por detecta inserções de seus próprio é relatada com a opção SQL_STATIC_SENSITIVITY **SQLGetInfo**.  
  
 A matriz de status de linha especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO ou SQL_ROW_ERROR para qualquer linha. Ele retorna SQL_ROW_UPDATED, SQL_ROW_DELETED ou SQL_ROW_ADDED para linhas que detecta como atualizado, excluído ou inserido.  
  
 Cursores controlados por conjunto de chaves geralmente são implementados por criar uma tabela temporária que contém as chaves para cada linha no conjunto de resultados. Como o cursor também deve determinar se linhas foram atualizadas, esta tabela contém também costuma ser uma coluna com informações de controle de versão de linha.  
  
 Para rolar ao longo do conjunto de resultados original, o cursor controlado por abre um cursor estático sobre a tabela temporária. Para recuperar uma linha no conjunto de resultados original, o cursor primeiro recupera a chave apropriada da tabela temporária e, em seguida, recupera os valores atuais para a linha. Se forem usados cursores em bloco, o cursor deve recuperar várias chaves e linhas.
