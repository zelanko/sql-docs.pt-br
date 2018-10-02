---
title: MSSQLSERVER_5243 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5243 (Database Engine error)
ms.assetid: e04a1934-e57d-420e-ac79-97071745824e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8919457cb10ae9feaa7e1c82eed5a73860fd6d42
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47829754"
---
# <a name="mssqlserver5243"></a>MSSQLSERVER_5243
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|5243|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Foi detectada uma inconsistência durante uma operação interna. Contate o suporte técnico. Número de referência %ld.|  
  
## <a name="explanation"></a>Explicação  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detectou uma inconsistência estrutural em uma estrutura do mecanismo de armazenamento na memória.  
  
## <a name="user-action"></a>Ação do usuário  
Procure falhas de hardware. Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do sistema Windows e do aplicativo, além do log de erros do SQL Server, para verificar se o erro ocorreu em decorrência de falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.

Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação em cache seja o problema, contate o fornecedor do hardware.

Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.

Restaure do backup. Se o problema não estiver relacionado ao hardware e um backup limpo conhecido estiver disponível, restaure o banco de dados do backup.

Execute DBCC CHECKDB Se nenhum backup limpo estiver disponível, execute DBCC CHECKDB sem a cláusula REPAIR para determinar a extensão do dano. DBCC CHECKDB recomendará uma cláusula REPAIR para ser usada. Execute DBCC CHECKDB com a cláusula REPAIR apropriada para reparar o dano.

> **não há suporte para a marca de alerta!**
>  **não há suporte para a marca de alerta!**
>  **não há suporte para a marca de alerta!**

Se a execução de DBCC CHECKDB com uma das cláusulas REPAIR não corrigir o problema, contate seu provedor de suporte.
  
## <a name="see-also"></a>Consulte Também  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[Arquivos e grupos de arquivos do banco de dados](~/relational-databases/databases/database-files-and-filegroups.md)  
  
