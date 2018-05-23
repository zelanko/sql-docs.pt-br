---
title: MSSQLSERVER_1105 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 1105 (Database Engine error)
ms.assetid: e7f4ad02-8c7f-4bb9-9781-2c86253f2138
caps.latest.revision: 19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ef9afa3f317c9a05f94f92c412e5139050e49603
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver1105"></a>MSSQLSERVER_1105
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
> Quando um índice está localizado em vários arquivos, **ALTER INDEX REORGANIZE** pode retornar um erro 1105 quando um desses arquivos estiver cheio. O processo de reorganização é bloqueado quando o processo tenta mover as linhas para o arquivo cheio. Para resolver essa limitação, execute um **ALTER INDEX REBUILD** em vez de **ALTER INDEX REORGANIZE** ou aumente o limite de aumento de arquivo de todos os arquivos que estão cheios.  
  
