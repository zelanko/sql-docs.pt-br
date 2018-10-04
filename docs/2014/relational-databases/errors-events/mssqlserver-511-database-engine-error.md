---
title: MSSQLSERVER_511 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 511 (Database Engine error)
ms.assetid: 0c85686a-53c1-4180-ba8c-2000e68a0d63
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ee53135fb492185d91287f553b7b1f0ddf3cc8ba
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48071686"
---
# <a name="mssqlserver511"></a>MSSQLSERVER_511
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|511|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|ROW_TOOBIG|  
|Texto da mensagem|Não é possível criar uma linha com o tamanho %d que seja maior que o máximo permitido de %d.|  
  
## <a name="explanation"></a>Explicação  
 A operação que você tentou excedeu o tamanho máximo de uma linha. Normalmente, o tamanho máximo de uma linha é de 8.060 bytes. Alguns formatos de armazenamento contêm sobrecarga que pode reduzir o tamanho de linha disponível para dados. Por exemplo, quando você usa colunas esparsas, o tamanho máximo de uma linha é de 8.018 bytes. Algumas operações que adicionam ou removem linhas e outras operações que alteram o tipo de dados de uma coluna exigem que a linha seja gravada novamente na página de dados e que a linha original seja posteriormente removida. Nessas operações, o limite efetivo do tamanho da linha é metade do limite máximo. Isso ocorre porque a linha original e a linha modificada devem ser incluídas na página de dados por um período curto.  
  
> [!WARNING]  
>  Cada coluna **varchar(max)** ou **nvarchar(max)** não nula exige 24 bytes de alocação fixa adicional, que conta para o limite de linha de 8.060 bytes durante uma operação de classificação. Isso pode criar um limite implícito para o número de colunas **varchar(max)** ou **nvarchar(max)** não nulas que podem ser criadas em uma tabela. Nenhum erro especial é fornecido quando a tabela é criada (além do aviso comum de que o tamanho máximo da linha excede o máximo permitido de 8060 bytes) ou no momento da inserção de dados. Esse tamanho de linha pode causar erros (por exemplo, o erro 512) durante algumas operações normais, como uma atualização de chave de índice clusterizado ou classificações do conjunto de colunas completo, que os usuários não podem prever até que uma operação seja executada.  
  
## <a name="user-action"></a>Ação do usuário  
 Se for possível, reduza o tamanho da linha.  
  
 Se considerar que o problema está sendo causado por uma atualização no local da linha, será necessário alterar a tabela em várias etapas. Crie uma tabela e transfira os dados para ela. Depois, exclua a tabela original e renomeie a tabela nova ou, então, trunque a tabela original, modifique as linhas na tabela original e, depois, mova os dados de volta para ela.  
  
  
