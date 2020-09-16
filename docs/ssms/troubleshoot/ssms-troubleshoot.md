---
description: Obter dados de diagnóstico após uma falha do SQL Server Management Studio (SSMS)
title: Solução de problemas em um sistema com falha ou sem resposta com o SSMS
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.reviewer: dnethi
ms.custom: seo-lt-2019
ms.date: 09/18/2019
ms.openlocfilehash: 2a6f7d1ac44b40b1b58ebe0a2a595e9f69f1ab63
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480058"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>Obter dados de diagnóstico após uma falha do SQL Server Management Studio (SSMS)

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

## <a name="get-full-memory-dump-after-an-unresponsive-system-or-crash"></a>Obter o despejo de memória completo após o sistema falhar ou ficar sem resposta

Obtenha o despejo de memória completo do SSMS (SQL Server Management Studio) quando ele falhar ou parar de responder.

Siga as etapas abaixo para capturar informações de diagnóstico para solucionar problemas de falha ou falta de resposta do SSMS.

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
