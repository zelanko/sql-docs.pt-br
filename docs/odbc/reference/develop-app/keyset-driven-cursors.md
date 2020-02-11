---
title: Cursores controlados por conjunto de chaves | Microsoft Docs
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
ms.openlocfilehash: 0c40fe8c823115c3131a1719185bce8f1506df81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138840"
---
# <a name="keyset-driven-cursors"></a>Cursores controlados por conjunto de chaves
Um cursor controlado por conjunto de chaves está entre um cursor estático e um curso dinâmico em sua capacidade de detectar alterações. Como um cursor estático, ele nem sempre detecta alterações à associação e à ordem do conjunto de resultados. Como um cursor dinâmico, ele detecta alterações nos valores de linhas no conjunto de resultados (sujeito ao nível de isolamento da transação, conforme definido pelo atributo de conexão SQL_ATTR_TXN_ISOLATION).  
  
 Quando um cursor controlado por conjunto de chaves é aberto, ele salva as chaves para todo o conjunto de resultados; isso corrige a associação aparente e a ordem do conjunto de resultados. À medida que o cursor percorre o conjunto de resultados, ele usa as chaves nesse *conjuntos de chaves* para recuperar os valores de dados atuais para cada linha. Por exemplo, suponha que um cursor controlado por conjunto de chaves busque uma linha e outro aplicativo, em seguida, atualize essa linha. Se o cursor buscar a linha novamente, os valores que ele vê serão os novos porque ele rebuscau a linha usando sua chave. Por isso, os cursores controlados por conjunto de chaves sempre detectam alterações feitas por si mesmos e por outras pessoas.  
  
 Quando o cursor tenta recuperar uma linha que foi excluída, essa linha aparece como um "buraco" no conjunto de resultados: a chave para a linha existe no conjuntos de chaves, mas a linha não existe mais no conjunto de resultados. Se os valores de chave em uma linha forem atualizados, a linha será considerada como excluída e, em seguida, inserida, portanto, essas linhas também aparecerão como buracos no conjunto de resultados. Embora um cursor controlado por conjunto de chaves sempre possa detectar linhas excluídas por outros, ele pode, opcionalmente, remover as chaves para as linhas que ele exclui do conjunto de chaves. Os cursores controlados por conjunto de chaves que fazem isso não podem detectar suas próprias exclusões. Se um determinado cursor controlado por conjunto de chaves detectar suas próprias exclusões é relatado por meio da opção SQL_STATIC_SENSITIVITY em **SQLGetInfo**.  
  
 As linhas inseridas por outras nunca são visíveis para um cursor controlado por conjunto de chaves porque não existem chaves para essas linhas no conjunto de chaves. No entanto, um cursor controlado por conjunto de chaves pode opcionalmente adicionar as chaves para as linhas que insere no conjunto de chaves. Os cursores controlados por conjunto de chaves que fazem isso podem detectar suas próprias inserções. Se um determinado cursor controlado por conjunto de chaves detectar suas próprias inserções é relatado por meio da opção SQL_STATIC_SENSITIVITY em **SQLGetInfo**.  
  
 A matriz de status de linha especificada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR pode conter SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO ou SQL_ROW_ERROR para qualquer linha. Ele retorna SQL_ROW_UPDATED, SQL_ROW_DELETED ou SQL_ROW_ADDED para as linhas detectadas como atualizadas, excluídas ou inseridas.  
  
 Os cursores controlados por conjunto de chaves são comumente implementados pela criação de uma tabela temporária que contém as chaves para cada linha no conjunto de resultados. Como o cursor também deve determinar se as linhas foram atualizadas, essa tabela normalmente também contém uma coluna com informações de controle de versão de linha.  
  
 Para rolar o conjunto de resultados original, o cursor controlado por conjunto de chaves abre um cursor estático sobre a tabela temporária. Para recuperar uma linha no conjunto de resultados original, o cursor primeiro recupera a chave apropriada da tabela temporária e, em seguida, recupera os valores atuais para a linha. Se os cursores de bloco forem usados, o cursor deverá recuperar várias chaves e linhas.
