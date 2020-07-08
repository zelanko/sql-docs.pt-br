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
ms.openlocfilehash: f6176b0e0f7c179c9817a65bb20d6370d83b2c23
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717011"
---
# <a name="mssqlserver_5243"></a>MSSQLSERVER_5243
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|5243|  
|Origem do Evento|MSSQLSERVER|  
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
> **não há suporte para a marca de alerta!** 
> **não há suporte para a marca de alerta!**

Se a execução de DBCC CHECKDB com uma das cláusulas REPAIR não corrigir o problema, contate seu provedor de suporte.
  
## <a name="see-also"></a>Consulte Também  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[Arquivos e grupos de arquivos do banco de dados](~/relational-databases/databases/database-files-and-filegroups.md)  
  
