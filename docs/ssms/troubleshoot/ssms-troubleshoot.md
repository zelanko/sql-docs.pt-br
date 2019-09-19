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
ms.openlocfilehash: e73e3d8cc0b54f0251530327dbcea941546471d5
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212437"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>Obter dados de diagnóstico após uma falha do SQL Server Management Studio (SSMS)

[!INCLUDE[Aplica-se a](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)

## <a name="get-full-memory-dump-after-a-hang-or-crash"></a>Obter o despejo de memória completo após uma falha ou travamento

Obtenha o despejo de memória completo no SSMS (SQL Server Management Studio) ao ocorrer falha ou travamento.

Siga as etapas abaixo para capturar informações de diagnóstico para solucionar problemas de falha ou travamento do SSMS.

1. Baixe o [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Descompacte-o em uma pasta.

3. Abra o Prompt de Comando e execute o comando a seguir.

    ```console
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    Se ele solicitar que você aceite um contrato de licença, selecione *Concordo*.

4. Inicie o SSMS, caso ele ainda não tenha sido iniciado.

5. Reproduza o problema.

6. O texto deve aparecer no prompt de comando sobre a gravação do arquivo de despejo, aguarde até que termine.

7. Crie uma nova pasta e copie o arquivo *.dmp que foi gravado para essa pasta.

8. Copie os seguintes arquivos na mesma pasta.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Compacte a pasta

## <a name="get-full-memory-dump-for-an-outofmemoryexception"></a>Obter um despejo de memória completo para uma OutOfMemoryException

Obtenha um despejo de memória completo do SSMS quando ele gerar uma OutOfMemoryException.

Você pode obter um despejo de memória completo com qualquer exceção gerenciada.

Para capturar as informações de diagnóstico a fim de solucionar problemas de OutOfMemoryException no SSMS, siga as etapas abaixo.

1. Baixe o [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Descompacte-o em uma pasta.

3. Abra o Prompt de Comando e execute o comando a seguir.

    ```console
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
