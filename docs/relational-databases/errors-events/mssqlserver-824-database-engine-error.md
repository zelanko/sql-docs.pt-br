---
description: MSSQLSERVER_824
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
ms.openlocfilehash: 0e2242b539f5fadb18beb54115e2cbad95336497
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499501"
---
# <a name="mssqlserver_824"></a>MSSQLSERVER_824
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|824|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|B_HARDSSERR|  
|Texto da mensagem|O SQL Server detectou um erro de E/S baseado em consistência lógica: %ls. Isso aconteceu durante um %S_MSG da página %S_PGID na ID de banco de dados %d no deslocamento %#016I64x no arquivo '%ls'.  Mensagens adicionais no log de erros ou no log de eventos do sistema no SQL Server poderão fornecer mais detalhes.|  
  
## <a name="symptom"></a>Sintoma  


Você poderá encontrar a seguinte mensagem de erro no log de erros do SQL Server ou no log de eventos do Aplicativo do Windows se uma verificação de consistência lógica falhar após ler ou gravar uma página do banco de dados:
 
``` 
2009-11-02 15:46:42.90 spid51      Error: 824, Severity: 24, State: 2.
2009-11-02 15:46:42.90 spid51      SQL Server detected a logical consistency-based I/O error: incorrect pageid (expected 1:43686; actual 0:0). It occurred during a read of page (1:43686) in database ID 23 at offset 0x0000001554c000 in file 'H:\MSSQL.SQL2008\MSSQL\DATA\my_db.mdf'.  Additional messages in the SQL Server error log or system event log may provide more detail. This is a severe error condition that threatens database integrity and must be corrected immediately. Complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.
```
 
Se um aplicativo encontrar essa mensagem ao consultar ou modificar dados, a mensagem de erro será retornada ao aplicativo e a conexão de banco de dados será encerrada. 
  
## <a name="cause"></a>Causa
Esse erro indica que o Windows informa que a página foi lida com êxito no disco, mas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] descobriu algo errado com a página. Esse erro é semelhante ao erro 823, exceto pelo fato de o Windows não ter detectado o erro. Normalmente, ele indica um problema no subsistema de E/S, como uma unidade de disco deficiente, problemas de firmware de disco, driver de dispositivo defeituoso e assim por diante. Para obter mais informações sobre erros de E/S, consulte [Microsoft SQL Server I/O Basics, Chapter 2](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)) (Noções básicas de E/S do Microsoft SQL Server, Capítulo 2).  

O SQL Server usa APIs do Windows, por exemplo, ReadFile, WriteFile, ReadFileScatter, WriteFileGather, para executar operações de E/S. Depois de executar essas operações de E/S, o SQL Server verifica se há quaisquer condições de erro associadas a essas chamadas à API. Se as chamadas à API falharem com um erro do sistema operacional, o SQL Server relatará o Erro 823. Pode haver situações em que a chamada à API do Windows foi bem-sucedida, mas os dados transferidos pela operação de E/S podem ter encontrado um problema de consistência lógica. Esses problemas de consistência lógica são relatados pelo Erro 824.
 
O erro 824 contém as seguintes informações:

- O arquivo de banco de dados no qual a operação de E/S é executada
- O deslocamento no arquivo em que ocorreu a tentativa de realização da operação de E/S
- O banco de dados ao qual o arquivo pertence
- O número da página que estava envolvida na operação de E/S
- Se a operação era de leitura ou de gravação
- Detalhes sobre a verificação de consistência lógica que falhou [o tipo de verificação, valor real e valor esperado usado para esta verificação]
 
Essas verificações de consistência lógica são verificações de integridade adicionais realizadas pelo SQL Server para garantir que determinados aspectos principais dos dados envolvidos na transferência de dados tenham sido mantidos em toda a operação de E/S. As verificações incluem soma de verificação, página interrompida, transferência curta, ID de página incorreta, leitura obsoleta, falha de auditoria de página. A natureza das verificações realizadas varia dependendo das diferentes opções de configuração no nível do banco de dados e do servidor. 
 
A mensagem de erro 824 geralmente indica que há um problema com o sistema de armazenamento subjacente, o hardware ou um driver que está no caminho da solicitação de E/S. Você poderá encontrar esse erro quando houver inconsistências no sistema de arquivos ou se o arquivo de banco de dados estiver danificado.

## <a name="resolution"></a>Resolução  

Se encontrar o erro 824, você poderá tentar as seguintes resoluções: 

- Examine a tabela [suspect_pages](../backup-restore/manage-the-suspect-pages-table-sql-server.md) no msdb para verificar se outras páginas (no mesmo banco de dados ou em bancos de dados diferentes) estão encontrando esse problema.
- Verifique a consistência dos bancos de dados localizados no mesmo volume (que o relatado na mensagem 824) usando o comando DBCC CHECKDB. Se você encontrar inconsistências do comando DBCC CHECKDB, use as diretrizes do artigo da base de dados de conhecimento [Como solucionar problemas de consistência do banco de dados relatados pelo DBCC CHECKDB](https://support.microsoft.com/help/2015748/how-to-troubleshoot-database-consistency-errors-reported-by-dbcc-check).
- Se o banco de dados que encontra esses erros 824 não tiver a opção PAGE_VERIFY CHECKSUM do banco de dados ativada, faça isso imediatamente. Erros 824 podem ocorrer por outros motivos além de uma falha de soma de verificação, mas CHECKSUM fornece a melhor opção para verificar a consistência da página depois que ela foi gravada no disco.
- Examine os logs de eventos do Windows para verificar se há erros ou mensagens relatadas pelo sistema operacional, um dispositivo de armazenamento ou um driver de dispositivo. Se eles estiverem relacionados a esse erro de alguma forma, resolva esses erros primeiro. Por exemplo, além da mensagem 824, você também poderá observar um evento como "O driver detectou um erro de controlador em \Device\Harddisk4\DR4" relatado pela origem do disco no log de eventos. Nesse caso, você precisará avaliar se esse arquivo está presente neste dispositivo e corrigir os erros de disco primeiro.
- Use o utilitário [SQLIOSim](https://support.microsoft.com/help/231619/how-to-use-the-sqliosim-utility-to-simulate-sql-server-activity-on-a-d) para descobrir se esses erros 824 poderão ser reproduzidos fora das solicitações regulares de E/S do SQL Server. O SQLIOSim é fornecido com o SQL Server 2008, de maneira que não há necessidade de um download separado nessa versão ou em versões posteriores.
- Trabalhe com o fabricante do dispositivo ou fornecedor de hardware para garantir que:
   - Os dispositivos de hardware e a configuração estejam em conformidade com os [requisitos de E/S do SQL Server](https://support.microsoft.com/help/967576/microsoft-sql-server-database-engine-input-output-requirements).
   - Os drivers de dispositivo e outros componentes de software de suporte de todos os dispositivos no caminho de E/S estejam atualizados.
- Se o fabricante do dispositivo ou fornecedor de hardware fornecer a você utilitários de diagnóstico, use-os para avaliar a integridade do sistema de E/S.
- Avalie se há Drivers de Filtro no caminho dessas solicitações de E/S que encontram problemas.
   - Verifique se há atualizações para esses drivers de filtro
   - Esses drivers de filtro podem ser removidos ou desabilitados para observar se o problema que resulta no erro 824 desaparece
- Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  

## <a name="see-also"></a>Consulte Também  
[Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](~/relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
