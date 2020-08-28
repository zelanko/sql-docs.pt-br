---
description: Cursores do conjunto de chaves
title: Cursores do conjunto de chaves | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Keyset cursors [ADO]
- cursors [ADO], Keyset
ms.assetid: 14b51b17-6fd9-4146-af45-ca4b0fe6d48a
author: rothja
ms.author: jroth
ms.openlocfilehash: 8c84bf798dcdb543dd0ae407474aa68cfb06a9ba
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980337"
---
# <a name="keyset-cursors"></a>Cursores do conjunto de chaves
O cursor do conjunto de chaves fornece funcionalidade entre um cursor estático e um curso dinâmico em sua capacidade de detectar alterações. Como um cursor estático, ele nem sempre detecta alterações à associação e à ordem do conjunto de resultados. Como um cursor dinâmico, ele detecta alterações aos valores de linhas no conjunto de resultados.  
  
 Os cursores controlados por conjuntos de chaves são controlados por um conjunto exclusivo de identificadores (chaves) conhecido como conjunto de chaves. As chaves são criadas a partir de um conjunto de colunas, que identificam exclusivamente as linhas no conjunto de resultados. O conjunto de chaves é o conjunto de valores de chave de todas as linhas retornadas pela instrução de consulta.  
  
 Com cursores controlados por conjunto de chaves, uma chave é criada e salva para cada linha do cursor e armazenada na estação de trabalho cliente ou no servidor. Quando você acessa cada linha, a chave armazenada é usada para buscar os valores de dados atual da fonte de dados. Em um cursor controlado por conjunto de chaves, a associação do conjunto de resultados é congelada quando o conjunto de chaves está completamente preenchido. Depois disso, adições ou atualizações que afetem a associação não farão parte do resultado definido até que ele seja reaberto.  
  
 As alterações nos valores de dados (feitas pelo proprietário do conjunto de chaves ou por outros processos) são visíveis à medida que o usuário rola por todo o resultado. Inserções feitas fora do cursor (por outros processos) serão visíveis apenas se o cursor for fechado e reaberto. Inserções feitas de dentro do cursor são visíveis no final do conjunto de resultados.  
  
 Quando um cursor controlado por conjunto de chaves tenta recuperar uma linha que foi excluída, a linha é exibida como um "buraco" no conjunto de resultados. A chave para a linha existe no conjunto de chaves, mas a linha não existe mais no conjunto de resultados. Se os valores de chave em uma linha forem atualizados, a linha será considerada como excluída e, em seguida, inserida, portanto, essas linhas também aparecerão como buracos no conjunto de resultados. Embora um cursor controlado por conjunto de chaves sempre possa detectar linhas excluídas por outros processos, ele pode, opcionalmente, remover as chaves para as linhas que ele exclui. Os cursores controlados por conjunto de chaves que fazem isso não podem detectar suas próprias exclusões porque a evidência foi removida.  
  
 Uma atualização para uma coluna de chave funciona como uma exclusão da chave antiga seguida de uma inserção da nova chave. O novo valor de chave não será visível se a atualização não tiver sido feita pelo cursor. Se a atualização tiver sido feita por meio do cursor, o novo valor de chave será visível no final do conjunto de resultados.  
  
 Há uma variação nos cursores controlados por conjunto de chaves chamados cursores padrão controlados por conjunto de chaves. Em um cursor padrão controlado por conjunto de chaves, a associação de linhas no conjunto de resultados e a ordem das linhas são fixas no tempo de abertura do cursor, mas as alterações nos valores que são feitas pelo proprietário do cursor e pelas alterações confirmadas feitas por outros processos são visíveis. Se uma alteração desqualificar uma linha para associação ou afetar a ordem de uma linha, a linha não desaparecerá ou será movida, a menos que o cursor seja fechado e reaberto. Os dados inseridos não são exibidos, mas as alterações nos dados existentes são exibidas à medida que as linhas são buscadas.  
  
 O cursor controlado por conjunto de chaves é difícil de usar corretamente porque a sensibilidade às alterações de dados depende de muitas circunstâncias diferentes, conforme descrito acima. No entanto, se seu aplicativo não estiver preocupado com atualizações simultâneas, o pode manipular chaves inadequadas de forma programática e deve acessar diretamente determinadas linhas com chave, o cursor controlado por conjunto de chaves pode funcionar para você. Use o **AdOpenKeyset CursorTypeEnum** para indicar que você deseja usar um cursor de conjunto de chaves no ADO.  
  
## <a name="see-also"></a>Consulte Também  
 [Cursores de somente avanço](./forward-only-cursors.md)   
 [Cursores estáticos](./static-cursors.md)   
 [Cursores dinâmicos](./dynamic-cursors.md)