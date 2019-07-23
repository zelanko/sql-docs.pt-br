---
title: Solução de problemas de um travamento ou falha com o SQL Server Management Studio (SSMS)
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: dnethi
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 07/01/2019
ms.openlocfilehash: 2011de961cc7f54a23b19928a7f6f9df8b962ac8
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262769"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>Obter dados de diagnóstico após uma falha do SQL Server Management Studio (SSMS)

[!INCLUDE[Aplica-se a](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)

## <a name="get-full-memory-dump-after-a-hang-or-crash"></a>Obter o despejo de memória completo após uma falha ou travamento

Obtenha o despejo de memória completo no SSMS (SQL Server Management Studio) ao ocorrer falha ou travamento.

Siga as etapas abaixo para capturar informações de diagnóstico para solucionar problemas de falha ou travamento do SSMS.

1. Baixe o [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Descompacte-o em uma pasta.

3. Abra o Prompt de Comando e execute o comando a seguir.

    '''command prompt  <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    If it prompts you to accept a license agreement, select *Agree*.

4. Start SSMS, if it hasn't started already.

5. Reproduce the issue.

6. The text should appear in the cmd prompt about writing the dump file, wait for that to finish.

7. Create a new folder and copy the *.dmp file that is written out to that folder.

8. Copy the following files into the same folder.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Zip up the folder

## Get full memory dump for an OutOfMemoryException

Get a full memory dump of SSMS when it throws an OutOfMemoryException.

You can get a full memory dump with any managed exception.

To capture diagnostic information to troubleshoot an OutOfMemoryException from SSMS, follow the steps below.

1. Download [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Unzip the download into a folder.

3. Open Command Prompt and run the following command.

    ```command prompt
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    Se ele solicitar que você aceite um contrato de licença, selecione *Concordo*.

4. Inicie o SQL Server Management Studio, se ainda não tiver iniciado.

5. Reproduza o problema.

6. O texto deve aparecer no prompt de comando sobre a gravação do arquivo de despejo, aguarde até que termine.

7. Crie uma nova pasta e copie o arquivo *.dmp que foi gravado para essa pasta.

8. Copie os seguintes arquivos na mesma pasta.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Compacte a pasta.