---
title: MSSQLSERVER_3156 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3156 (Database Engine error)
ms.assetid: 345d8ed4-177e-4ec3-bab3-25d30000e323
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5480f60c6bb47f5e2c0a03236da30a7dada30209
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723727"
---
# <a name="mssqlserver_3156"></a>MSSQLSERVER_3156
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|3156|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|LDDB_CANT_WRITE|  
|Texto da mensagem|O arquivo '%ls' não pode ser restaurado para '%ls'. Use WITH MOVE para identificar um local válido para o arquivo.|  
  
## <a name="explanation"></a>Explicação  
Esta mensagem geral identifica os nomes de arquivo lógicos ou físicos dos arquivos que não puderam ser restaurados devido a um problema com o local especificado.  
  
### <a name="possible-causes"></a>Possíveis causas  
As causas possíveis incluem as seguintes:  
  
-   Talvez seja preciso acessar o diretório especificado do Windows.  
  
-   Você pode ter digitado incorretamente o caminho ou pode ter especificado um caminho que não existe.  
  
-   O nome de arquivo pode estar sendo usado por um arquivo que não pode ser substituído.  
  
## <a name="user-action"></a>Ação do usuário  
Veja nos logs de erros outras mensagens mais detalhadas.  
  
Corrija o problema com o local especificado, por exemplo, concedendo acesso, ou use a opção WITH MOVE em sua instrução RESTORE para realocar o arquivo.  
  
## <a name="see-also"></a>Consulte Também  
[Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[Restaurar arquivos em um novo local &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
