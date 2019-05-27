---
title: Obter o despejo de memória completo para solucionar problemas do SSMS (SQL Server Management Studio)
Description: Solução de problemas de um travamento ou uma falha do SSMS ao coletar um despejo de memória completo
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: how-to
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: dineth, sstein
ms.custom: ''
ms.date: 05/17/2019
ms.openlocfilehash: ff78af4ffcfe530ba28d47ec57852486523f859a
ms.sourcegitcommit: c29150492383f48ef484fa02a483cde1cbc68aca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2019
ms.locfileid: "65822504"
---
# <a name="get-full-memory-dump"></a>Obtenha Despejo de Memória Completo

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

Neste artigo, você aprenderá a capturar informações de diagnóstico para solucionar problemas de uma falha ou travamento ocorrido com o SSMS (SQL Server Management Studio).

Siga as etapas abaixo para capturar informações de diagnóstico para solucionar problemas.

1. Baixe o [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Descompacte-o em uma pasta.

3. Abra o Prompt de Comando e execute o comando a seguir.

    ```cmd
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    Ele solicitará que você aceite um contrato de licença, selecione **Concordo**.

4. Inicie o SSMS, se ainda não tiver iniciado.

5. Reproduza o problema.

6. O texto deve aparecer no prompt de comando sobre a gravação do arquivo de despejo, aguarde até que termine.

7. Crie uma nova pasta e copie o arquivo *.dmp que foi gravado para essa pasta.

8. Copie os seguintes arquivos na mesma pasta.

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Compacte a pasta.

## <a name="outofmemoryexception"></a>OutOfMemoryException

Você também pode obter o despejo de memória completo do SSMS quando ele gera uma OutOfMemoryException (pode ser qualquer exceção gerenciada).

Siga as etapas abaixo para capturar informações de diagnóstico para solucionar problemas de uma OutOfMemoryException do SSMS.

1. Baixe o [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Descompacte-o em uma pasta.

3. Abra o Prompt de Comando e execute o comando a seguir.

    ```cmd
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    Ele solicitará que você aceite um contrato de licença, selecione **Concordo**.

4. Inicie o SQL Server Management Studio, se ainda não tiver iniciado.

5. Reproduza o problema.

6. O texto deve aparecer no prompt de comando sobre a gravação do arquivo de despejo, aguarde até que termine.

7. Crie uma nova pasta e copie o arquivo *.dmp que foi gravado para essa pasta.

8. Copie os seguintes arquivos na mesma pasta.

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Compacte a pasta.

## <a name="next-steps"></a>Próximas etapas

[SQL Server Management Studio](../sql-server-management-studio-ssms.md)