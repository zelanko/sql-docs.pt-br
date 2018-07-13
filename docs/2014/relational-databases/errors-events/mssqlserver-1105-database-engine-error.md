---
title: MSSQLSERVER_1105 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 1105 (Database Engine error)
ms.assetid: e7f4ad02-8c7f-4bb9-9781-2c86253f2138
caps.latest.revision: 20
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0d7a22dc333f2e4acf5f56553a188199cbf08571
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420675"
---
# <a name="mssqlserver1105"></a>MSSQLSERVER_1105
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|1105|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NO_MORE_SPACE_IN_FG|  
|Texto da mensagem|Não foi possível alocar espaço ao objeto '%.*ls'%.\*ls no banco de dados '%.\*ls' porque o grupo de arquivos '%.\*ls' está cheio. Crie espaço em disco excluindo arquivos desnecessários, descartando objetos no grupo de arquivos, adicionando arquivos ao grupo de arquivos ou definindo o aumento automático para arquivos existentes no grupo de arquivos.|  
  
## <a name="explanation"></a>Explicação  
 Não há espaço disponível em disco em um grupo de arquivos.  
  
## <a name="user-action"></a>Ação do usuário  
 As seguintes ações podem criar espaço disponível no grupo de arquivos:  
  
-   Ative o aumento automático.  
  
-   Adicione mais arquivos ao grupo de arquivos.  
  
-   Libere espaço em disco descartando índices ou tabelas que não sejam mais necessários.  
  
-   Para obter mais informações, consulte “Solucionando problemas de espaço de dados insuficiente no disco” nos Manuais Online do SQL Server.  
  
> [!NOTE]  
>  Quando um índice encontra-se em vários arquivos, o `ALTER INDEX REORGANIZE` pode retornar um erro 1105 quando um desses arquivos estiver cheio. O processo de reorganização é bloqueado quando o processo tenta mover as linhas para o arquivo cheio. Como alternativa a esta limitação, execute um `ALTER INDEX REBUILD` em vez de `ALTER INDEX REORGANIZE` ou aumente o limite de crescimento dos arquivos cheios.  
  
  
