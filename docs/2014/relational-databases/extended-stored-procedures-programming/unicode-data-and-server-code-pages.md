---
title: Dados Unicode e páginas de código do servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- metadata [SQL Server], stored procedures
- Unicode [SQL Server], extended stored procedures
- extended stored procedures [SQL Server], metadata
ms.assetid: 52310260-a892-4b27-ad2e-bf164b98ee80
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b7c992f8b33e2eb96b0e6ea7eec1f58beaf8aefd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62511821"
---
# <a name="unicode-data-and-server-code-pages"></a>Páginas de código do servidor e dados Unicode
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 A API de procedimento armazenado estendido é habilitada para dados Unicode; porém, não é habilitada para metadados Unicode. O diretiva Unicode #define não tem nenhum efeito sobre a API de procedimento armazenado estendido.  
  
 Pressupõe-se que todos os metadados retornados pela API de procedimento armazenado estendido ou fornecidos para ela pelo seu aplicativo de procedimento armazenado estendido estejam na página de código multibyte do servidor. A página de código padrão de um aplicativo de servidor de API de procedimento armazenado estendido é a página de código ANSI do computador no qual o aplicativo está sendo executado, que pode ser obtido chamando **srv_pfield** com o parâmetro de campo definido como SRV_SPROC_CODEPAGE.  
  
 Se seu aplicativo de API de procedimento armazenado estendido for compatível com Unicode, você deverá converter os nomes das colunas de metadados Unicode, as mensagens de erro e assim por diante em dados multibyte antes de passar esses dados para a API de procedimento armazenado estendido.  
  
## <a name="example"></a>Exemplo  
 O procedimento armazenado estendido a seguir fornece um exemplo de conversões de Unicode. Observe que:  
  
-   Os dados da coluna são passados como dados Unicode para **srv_describe** porque a coluna está descrita como SRVNVARCHAR.  
  
-   Os metadados de nome de coluna são passados para **srv_describe** como dados multibyte.  
  
     O procedimento armazenado estendido chama **srv_pfield** com o parâmetro Field definido como SRV_SPROC_CODEPAGE para obter a página de código [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]multibyte de.  
  
-   As mensagens de erro são passadas para **srv_sendmsg** como dados multibyte.  
  
    ```  
    __declspec(dllexport) RETCODE proc1 (SRV_PROC *srvproc)  
    {  
        #define MAX_COL_NAME_LEN 25  
        #define MAX_COL_DATA_LEN 50  
        #define MAX_ERR_MSG_LEN 250  
        #define MAX_SERVER_ERROR 20000  
        #define XP_ERROR_NUMBER MAX_SERVER_ERROR+1  
  
        int retval;  
        UINT serverCodePage;  
        CHAR *szServerCodePage;  
  
        WCHAR unicodeColumnName[MAX_COL_NAME_LEN];  
        CHAR multibyteColumnName[MAX_COL_NAME_LEN];  
  
        WCHAR unicodeColumnData[MAX_COL_DATA_LEN];  
  
        WCHAR unicodeErrorMessage[MAX_ERR_MSG_LEN];  
        CHAR  multibyteErrorMessage[MAX_ERR_MSG_LEN];  
  
        lstrcpyW (unicodeColumnName, L"column1");  
        lstrcpyW (unicodeColumnData, L"column1 data");  
        lstrcpyW (unicodeErrorMessage, L"No Error!");  
  
        // Obtain server code page.  
        //  
        szServerCodePage = srv_pfield (srvproc, SRV_SPROC_CODEPAGE, NULL);      
        if (NULL != szServerCodePage)  
            serverCodePage = atol(szServerCodePage);  
        else   
        {   // Problem situation exists.  
            srv_senddone(srvproc, (SRV_DONE_ERROR | SRV_DONE_MORE), 0, 0);  
            return 1;  
        }  
  
        // Convert column name for Unicode to multibyte using the   
        // server code page.  
        //  
        retval = WideCharToMultiByte(    
            serverCodePage,                 // code page  
            0,                              // default  
            unicodeColumnName,              // wide-character string  
            -1,                             // string is null terminated  
            multibyteColumnName,            // address of buffer for new  
                                            //   string  
            sizeof (multibyteColumnName),   // size of buffer  
            NULL, NULL);  
  
        if (0 == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"Conversion to multibyte  
            failed.");  
            goto Error;  
        }  
  
        retval = srv_describe (srvproc, 1, multibyteColumnName,  
        SRV_NULLTERM,   
          SRVNVARCHAR, MAX_COL_DATA_LEN*sizeof(WCHAR), // destination  
            SRVNVARCHAR, lstrlenW(unicodeColumnData)*sizeof(WCHAR),  
            unicodeColumnData); //source  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_describe failed.");  
            goto Error;  
        }  
  
       retval = srv_sendrow(srvproc);  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_sendrow failed.");  
            goto Error;  
        }  
  
        retval = srv_senddone (srvproc, SRV_DONE_MORE|SRV_DONE_COUNT, 0, 1);  
        if (FAIL == retval)  
        {  
            lstrcpyW (unicodeErrorMessage, L"srv_senddone failed.");  
            goto Error;  
        }  
  
        return 0;  
    Error:  
        // convert error message from Unicode to multibyte.  
        retval = WideCharToMultiByte(    
            serverCodePage,                 // code page  
            0,                              // default  
            unicodeErrorMessage,            // wide-character string  
            -1,                             // string is null terminated  
            multibyteErrorMessage,          // address of buffer for new  
                                            //   string  
            sizeof (multibyteErrorMessage), // size of buffer  
            NULL, NULL);  
  
    srv_sendmsg(srvproc, SRV_MSG_ERROR, XP_ERROR_NUMBER, SRV_INFO, 1,  
                NULL, 0, __LINE__,   
                multibyteErrorMessage,  
                SRV_NULLTERM);  
  
        srv_senddone(srvproc, (SRV_DONE_ERROR | SRV_DONE_MORE), 0, 0);  
  
        return 1;  
    }  
  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [srv_wsendmsg &#40;API de procedimento armazenado estendido&#41;](../extended-stored-procedures-reference/srv-wsendmsg-extended-stored-procedure-api.md)  
  
  
