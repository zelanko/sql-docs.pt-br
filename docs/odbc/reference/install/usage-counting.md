---
title: Contagem de uso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- usage counts [ODBC]
- file usage counts [ODBC]
- installing ODBC components [ODBC], usage counts
- subkeys [ODBC], usage counts
ms.assetid: 0678aee9-8256-463c-89dd-77b1a0dfdd60
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca2a52eb08cdf1b1b9cb5a23805da34aab915b7a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47664624"
---
# <a name="usage-counting"></a>Contagem de uso
> [!NOTE]  
>  Começando com o Windows XP e Windows Server 2003, ODBC está incluído no sistema operacional Windows. Você deve instalar apenas explicitamente ODBC em versões anteriores do Windows.  
  
 Dois tipos de contagens de uso são mantidos no registro para cada componente: uma contagem de uso do componente e um ou mais contagens de uso de arquivo opcional. A contagem de uso do componente ajuda o instalador DLL manter as entradas do registro. Ele é armazenado no valor UsageCount sob o núcleo de ODBC, driver e subchaves de tradução. Para o formato do valor UsageCount e obter mais informações sobre essas subchaves, consulte [entradas do registro para componentes ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md).  
  
 Quando um componente é instalado pela primeira vez, o instalador DLL cria uma subchave para ele e define os dados para o valor de UsageCount nessa subchave como 1. Quando o componente é instalado novamente, a DLL do instalador incrementa a contagem de uso. Quando o componente for removido, o instalador DLL diminui o uso de contagem. Se a contagem de uso cair a 0, a DLL do instalador remove a subchave do componente.  
  
> [!CAUTION]  
>  Um aplicativo não deve fisicamente remover arquivos do Gerenciador de Driver quando a contagem de uso do componente e a contagem de utilização do arquivo atingir zero.  
  
 Contagens de ajudar a determinar quando um arquivo deve realmente ser copiado ou excluído como uso do arquivo em vez de incrementar ou diminuir a contagem de uso. Isso é importante porque os componentes ODBC e, portanto, os arquivos de componentes ODBC são compartilhados e podem ser instalados ou removidos por uma variedade de aplicativos. O aplicativo pode excluir arquivos de driver e translator se a contagem de uso do componente e a contagem de utilização do arquivo chegarem a zero. Arquivos do Gerenciador de driver não deveria, no entanto, ser excluído quando a contagem de uso do componente e a contagem de uso de arquivos têm chegou a zero, porque esses arquivos podem ser usados por outros aplicativos que não têm aumentado a contagem de uso de arquivos.  
  
> [!NOTE]  
>  Contagens de uso de arquivo são opcionais no Microsoft® WindowsNT®/Windows2000.  
  
 Contagens de uso de arquivo são mantidas pelo programa de instalação depois que ele chama **SQLInstallDriverManager**, **SQLInstallDriverEx**, **SQLInstallTranslatorEx**, **SQLRemoveDriverManager**, **SQLRemoveDriver**, ou **SQLRemoveTranslator**.  
  
 Quando um componente é instalado pela primeira vez, o instalador ou o programa de instalação DLL cria um valor na seguinte chave para cada arquivo no componente que não ainda esteja no sistema:  
  
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
  
 Ele define os dados para obter esses valores como 1 e copia o arquivo para o sistema. Quando o componente é instalado novamente, o programa de instalação ou a DLL do instalador incrementa as contagens de uso. Quando o componente for removido, diminui DLL de instalador ou o programa de instalação de contagens de uso. Se qualquer contagem de uso cair para 0, o programa de instalação ou a DLL do instalador remove o valor para o arquivo e, se o componente é um driver ou um conversor, exclui o arquivo. Arquivos de Gerenciador de driver não devem ser excluídos.  
  
 O formato do valor de contagem de uso do arquivo é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|data|  
|----------|---------------|----------|  
|*caminho completo*|REG_DWORD|*contagem*|  
  
 Por exemplo, suponha que um driver para o Informix usa os arquivos Infrmx32.dll e Infrmx32.hlp e suponha que esse driver foi instalado duas vezes. Os valores na subchave do driver Informix SharedDlls seria da seguinte maneira:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
