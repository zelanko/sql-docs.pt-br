---
title: MSSQLSERVER_21889 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21889 (Database Engine error)
ms.assetid: ae199540-7986-4cc2-b782-cd22793236d3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6ff8af9c4abe6f2784f153f8d8346b2609d3197b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780513"
---
# <a name="mssqlserver_21889"></a>MSSQLSERVER_21889
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|21889|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21889|  
|Texto da mensagem|A instância do SQL Server '% s' não é um publicador de replicação. Execute **sp_adddistributor** na instância '%s' do SQL Server com o distribuidor '%s' para permitir que a instância hospede o banco de dados de publicação '%s'. Certifique-se de especificar as mesmas informações de logon e senha que foram usadas para o publicador original.|  
  
## <a name="explanation"></a>Explicação  
Para hospedar o banco de dados publicador, a instância do SQL Server deve ser um publicador de replicação. **sp_validate_redirected_publisher** chama **sp_helpdistributor** no servidor remoto para determinar se o servidor é um publicador de replicação. Esse erro indica que a instância de destino do SQL Server não é um publicador de replicação.  
  
## <a name="user-action"></a>Ação do usuário  
Execute **sp_adddistributor** na instância do SQL Server que hospeda o banco de dados publicador. Ao executar **sp_adddistributor**, especifique o distribuidor correto. Use o mesmo valor para o parâmetro *\@password* usado quando **sp_adddistributor** foi executado inicialmente no distribuidor.  
  
