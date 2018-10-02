---
title: MSSQLSERVER_824 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 824 (Database Engine error)
ms.assetid: 2aa22246-2712-4fdb-9744-36e7e6f3175e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0773573e2b290b75bdc9855aa09f30a73be4197
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47597652"
---
# <a name="mssqlserver824"></a>MSSQLSERVER_824
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|824|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|B_HARDSSERR|  
|Texto da mensagem|O SQL Server detectou um erro de E/S baseado em consistência lógica: %ls. Isso aconteceu durante um %S_MSG da página %S_PGID na ID de banco de dados %d no deslocamento %#016I64x no arquivo '%ls'.  Mensagens adicionais no log de erros ou no log de eventos do sistema no SQL Server poderão fornecer mais detalhes.|  
  
## <a name="explanation"></a>Explicação  
Esse erro indica que o Windows informa que a página foi lida com êxito no disco, mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] descobriu algo errado com a página. Esse erro é semelhante ao erro 823, exceto pelo fato de o Windows não ter detectado o erro. Ele normalmente indica um problema no subsistema de E/S, como uma unidade de disco deficiente, problemas de firmware de disco, driver de dispositivo defeituoso e assim por diante. Para obter mais informações sobre erros de E/S, consulte [Microsoft SQL Server I/O Basics, Chapter 2](http://go.microsoft.com/fwlink/?LinkId=69370) (Noções básicas de E/S do Microsoft SQL Server, Capítulo 2).  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ver se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
Experimente mudar os bancos de dados para usar a opção PAGE_VERIFY CHECKSUM. Para obter informações sobre PAGE_VERIFY, consulte [ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](~/relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
