---
title: Contagem de uso | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0f9db5a35b8b0bb3dc437dd203267c6f53825e22
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="usage-counting"></a>Contagem de uso
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Instale somente explicitamente ODBC em versões anteriores do Windows.  
  
 Dois tipos de contagens de uso são mantidos no registro para cada componente: uma contagem de uso do componente e contagens de uso de arquivo opcional de um ou mais. A contagem de uso do componente ajuda o instalador DLL Manter entradas do registro. Ele é armazenado no valor UsageCount sob o núcleo de ODBC, driver e subchaves de conversor. Para o formato do valor UsageCount e obter mais informações sobre essas subchaves, consulte [entradas do registro para componentes ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md).  
  
 Quando um componente é instalado pela primeira vez, o instalador DLL cria uma subchave para ele e define os dados para o valor de UsageCount que subchave para 1. Quando o componente é instalado novamente, o instalador DLL incrementa a contagem de uso. Quando o componente é removido, o diminui DLL do instalador a utilização de contagem. Se a contagem de uso cair para 0, o instalador DLL remove a subchave para o componente.  
  
> [!CAUTION]  
>  Um aplicativo não deve fisicamente remover arquivos do Gerenciador de Driver quando a contagem de uso do componente e a contagem de uso de arquivo chegarem a zero.  
  
 Uso do arquivo de contagens de ajudar a determinar quando um arquivo deve realmente ser copiado ou excluído como oposição aumentando ou diminuindo a contagem de uso. Isso é importante porque os componentes ODBC e, portanto, os arquivos de componentes ODBC, são compartilhados e podem ser instalados ou removidos por uma variedade de aplicativos. O aplicativo pode excluir os arquivos de driver e o conversor se a contagem de uso do componente e a contagem de uso de arquivo chegarem a zero. Arquivos do Gerenciador de driver não deve, no entanto, ser excluído quando a contagem de uso do componente e a contagem de uso do arquivo atingiu zero, porque esses arquivos podem ser usados por outros aplicativos que não têm incrementado a contagem de uso de arquivos.  
  
> [!NOTE]  
>  Contagens de uso do arquivo são opcionais no Microsoft® WindowsNT®/Windows2000.  
  
 Contagens de uso do arquivo são mantidas pelo programa de instalação depois que ele chama **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **No SQLRemoveDriverManager**, **no SQLRemoveDriver**, ou **no SQLRemoveTranslator**.  
  
 Quando um componente é instalado pela primeira vez, o programa de instalação ou um instalador DLL cria um valor na seguinte chave para cada arquivo no componente que não esteja no sistema:  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  SOFTWARE  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  SharedDlls  
  
 Define os dados para os valores 1 e copia o arquivo para o sistema. Quando o componente é instalado novamente, o programa de instalação ou a DLL do instalador incrementa a contagem de uso. Quando o componente é removido, diminui DLL de programa ou de instalação do programa de instalação de contagens de uso. Se qualquer contagem de uso cair para 0, o programa de instalação ou a DLL do instalador remove o valor para o arquivo e, se o componente é um driver ou um conversor, exclui o arquivo. Arquivos do Gerenciador de driver não devem ser excluídos.  
  
 O formato do valor da contagem de uso de arquivo é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|*caminho completo*|REG_DWORD|*contagem*|  
  
 Por exemplo, suponha que um driver para Informix usa os arquivos Infrmx32.dll e Infrmx32.hlp e suponha que este driver foi instalado duas vezes. Os valores na subchave SharedDlls para o driver Informix seria a seguinte:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```

