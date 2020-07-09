---
title: Erro MSSQLSERVER 823 | mssqlserver_823
description: Uma descrição e algumas soluções comuns para o Erro Microsoft SQL Server 823 (mssqlserver_823), que é uma condição de erro grave no nível do sistema que ameaça a integridade do banco de dados e deve ser resolvida imediatamente.
ms.custom: ''
ms.date: 01/27/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 57850e8b54ef0f99895e558616b22089af266895
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767859"
---
# <a name="mssqlserver-error-823"></a>Erro MSSQLSERVER 823
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|823|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|B_HARDERR|  
|Texto da mensagem|O sistema operacional retornou o erro %ls para o SQL Server durante um %S_MSG no deslocamento %#016I64x do arquivo '%ls'. Additional messages in the SQL Server error log and system event log may provide more detail. Essa é uma condição de erro grave em nível de sistema que ameaça a integridade do banco de dados e deve ser corrigida imediatamente. Faça uma verificação completa da consistência do banco de dados (DBCC CHECKDB). Esse erro pode ter sido causado por vários fatores. Para obter mais informações, consulte os Manuais Online do SQL Server.|  
  
## <a name="explanation"></a>Explicação  
O SQL Server usa APIs do Windows (por exemplo, [ReadFile](/windows/win32/api/fileapi/nf-fileapi-readfile), [WriteFile](/windows/win32/api/fileapi/nf-fileapi-writefile), [ReadFileScatter](/windows/win32/api/fileapi/nf-fileapi-readfilescatter), [WriteFileGather](/windows/win32/api/fileapi/nf-fileapi-writefilegather)) para executar operações de E/S de arquivo. Depois de executar essas operações de E/S, o SQL Server verifica se há quaisquer condições de erro associadas a essas chamadas à API. Se as chamadas à API falharem com um erro do sistema operacional, o SQL Server relatará o Erro 823.

 A mensagem de erro 823 contém as seguintes informações:
 - O arquivo de banco de dados no qual a operação de E/S foi executada
 - O deslocamento dentro do arquivo em que ocorreu a tentativa de realização da operação de E/S. Esse é o deslocamento de bytes físicos do início do arquivo. Dividir esse número por 8192 fornecerá o número da página lógica afetada pelo erro.
 - Se a operação de E/S é uma solicitação de leitura ou gravação
 - O código de erro do sistema operacional e a descrição do erro entre parênteses
 

**Erro do sistema operacional:** Uma chamada à API do Windows de leitura ou gravação não foi bem-sucedida e o SQL Server encontra um erro do sistema operacional relacionado à chamada à API do Windows. A seguinte mensagem é um exemplo de um erro 823:

```
Error: 823, Severity: 24, State: 2.
2010-03-06 22:41:19.55 spid58 The operating system returned error 1117 (The request could not be performed because of an I/O device error.) to SQL Server during a read at offset 0x0000002d460000 in file 'e:\program files\Microsoft SQL Server\mssql\data\mydb.MDF'. Additional messages in the SQL Server error log and system event log may provide more detail. This is a severe, system-level error condition that threatens database integrity and must be corrected immediately. It is recommended to complete a full database consistency check (DBCC CHECKDB). This error can be caused by many factors; for more information, see SQL Server Books Online.
```

Você pode ou não ver erros da instrução DBCC CHECKDB no banco de dados associado ao arquivo na mensagem de erro. Você pode executar a instrução DBCC CHECKDB quando vir um erro 823. Se a instrução DBCC CHECKDB não relatar erros, você provavelmente terá um problema de sistema intermitente ou um problema de disco.

Informações de diagnóstico adicionais para erros 823 podem ser gravadas no arquivo de log de erros do SQL Server quando você usa o sinalizador de rastreamento 818.
Para obter mais informações, confira [KB 826433: Diagnóstico do SQL Server adicionado para detectar problemas de E/S não reportados](https://support.microsoft.com/help/826433/sql-server-diagnostics-added-to-detect-unreported-i-o-problems-due-to)


## <a name="cause"></a>Causa
A mensagem de erro 823 geralmente indica que há um problema com o sistema de armazenamento subjacente, o hardware ou um driver que está no caminho da solicitação de E/S. Você poderá encontrar esse erro quando houver inconsistências no sistema de arquivos ou se o arquivo de banco de dados estiver danificado. No caso de uma leitura de arquivo, o SQL Server já terá tentado novamente a solicitação de leitura quatro vezes antes de retornar o 823. Se a operação de repetição tiver êxito, a consulta não falhará, mas a mensagem [825](mssqlserver-825-database-engine-error.md) será gravada no ERRORLOG e no Log de eventos.

## <a name="user-action"></a>Ação do usuário  
 - Examine a tabela [suspect_pages](../system-tables/suspect-pages-transact-sql.md) no MSDB para outras páginas que estão encontrando esse problema (no mesmo banco de dados ou em bancos de dados diferentes).
 - Verifique a consistência dos bancos de dados localizados no mesmo volume (como o relatado na mensagem 823) usando o comando DBCC CHECKDB. Se você encontrar inconsistências do comando DBCC CHECKDB, use as diretrizes de [Como solucionar problemas de consistência do banco de dados relatados pelo DBCC CHECKDB](https://support.microsoft.com/help/2015748/how-to-troubleshoot-database-consistency-errors-reported-by-dbcc-check). 
 - Examine os logs de eventos do Windows para verificar se há erros ou mensagens relatadas pelo sistema operacional, um dispositivo de armazenamento ou um driver de dispositivo. Se eles estiverem relacionados a esse erro de alguma maneira, resolva esses erros primeiro. Por exemplo, além da mensagem 823, você também pode observar um evento como "O driver detectou um erro de controlador em \Device\Harddisk4\DR4" relatado pela origem do disco no log de eventos. Nesse caso, você precisará avaliar se esse arquivo está presente neste dispositivo e corrigir os erros de disco primeiro.
 - Use o utilitário [SQLIOSim](https://support.microsoft.com/help/231619/how-to-use-the-sqliosim-utility-to-simulate-sql-server-activity-on-a-d) para descobrir se esses erros 823 podem ser reproduzidos fora das solicitações regulares de E/S do SQL Server. O utilitário SQLIOSim é fornecido com o SQL Server 2008 e versões posteriores para que não haja necessidade de um download separado. Normalmente, você pode encontrá-lo na pasta `C:\Program Files\Microsoft SQL Server\MSSQLxx.MSSQLSERVER\MSSQL\Binn`.
 - Trabalhe com o fabricante do dispositivo ou fornecedor de hardware para garantir que
   - Os dispositivos de hardware e a configuração estejam em conformidade com os requisitos de E/S do SQL Server
   - Os drivers de dispositivo e outros componentes de software de suporte de todos os dispositivos no caminho de E/S estejam atualizados
 - Se o fabricante do dispositivo ou fornecedor de hardware fornecer a você utilitários de diagnóstico, use-os para avaliar a integridade do sistema de E/S
 - Avalie se há [drivers de filtro](https://support.microsoft.com/help/2454053/use-of-system-filter-drivers-can-lead-to-sql-server-database-engine-pe) no caminho dessas solicitações de E/S que encontram problemas.
   - Verifique se há atualizações para esses drivers de filtro
   - Esses drivers de filtro podem ser removidos ou desabilitados para observar se o problema que resulta no erro 823 desaparece  
