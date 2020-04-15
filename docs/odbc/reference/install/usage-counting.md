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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8d516a591bfde47522c0ccfe08bd2bd706218e07
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296016"
---
# <a name="usage-counting"></a>Contagem de uso
> [!NOTE]  
>  Começando com o Windows XP e o Windows Server 2003, o ODBC está incluído no sistema operacional windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 Dois tipos de contagem de uso são mantidos no registro de cada componente: uma contagem de uso de componentes e uma ou mais contagens opcionais de uso de arquivos. A contagem de uso do componente ajuda o instalador DLL a manter entradas de registro. Ele é armazenado no valor UseCount sob as subteclas ODBC Core, driver e tradutor. Para obter o formato do valor UseCount e mais informações sobre essas subchaves, consulte [Entradas de registro para componentes ODBC](../../../odbc/reference/install/registry-entries-for-odbc-components.md).  
  
 Quando um componente é instalado pela primeira vez, o instalador DLL cria uma subchave para ele e define os dados para o valor UseCount nessa subchave para 1. Quando o componente é instalado novamente, o instalador DLL aumenta a contagem de uso. Quando o componente é removido, o instalador DLL decreta a contagem de uso. Se a contagem de uso cair para 0, o instalador DLL removerá a subchave do componente.  
  
> [!CAUTION]  
>  Um aplicativo não deve remover fisicamente arquivos do Driver Manager quando a contagem de uso do componente e a contagem de uso do arquivo atingirem zero.  
  
 A contagem de uso de arquivos ajuda a determinar quando um arquivo deve realmente ser copiado ou excluído em vez de incrementar ou diminuir a contagem de uso. Isso é importante porque os componentes ODBC e, portanto, os arquivos em componentes ODBC, são compartilhados e podem ser instalados ou removidos por uma variedade de aplicativos. O aplicativo pode excluir arquivos de driver e tradutor se a contagem de uso do componente e a contagem de uso do arquivo chegar a zero. Os arquivos do Driver Manager não devem, no entanto, ser excluídos quando a contagem de uso do componente e a contagem de uso do arquivo atingirem zero, porque esses arquivos podem ser usados por outros aplicativos que não aumentaram a contagem de uso do arquivo.  
  
> [!NOTE]  
>  As contagens de uso de arquivos são opcionais no Microsoft® WindowsNT®/Windows2000.  
  
 As contagens de uso de arquivos são mantidas pelo programa de configuração depois que ele chama **SQLInstallDriverManager,** **SQLInstallDriverEx,** **SQLInstallTranslatorEx,** **SQLRemoveDriverManager,** **SQLRemoveDriver**ou **SQLRemoveTranslator**.  
  
 Quando um componente é instalado pela primeira vez, o programa de configuração ou o instalador DLL cria um valor sob a seguinte chave para cada arquivo nesse componente que ainda não está no sistema:  
  
> [!NOTE]  
>  HKEY_LOCAL_MACHINE  
>   
>  Software  
>   
>  Microsoft  
>   
>  Windows  
>   
>  CurrentVersion  
>   
>  Ddílios compartilhados  
  
 Ele define os dados desses valores para 1 e copia o arquivo para o sistema. Quando o componente é instalado novamente, o programa de configuração ou instalador DLL aumenta as contagens de uso. Quando o componente é removido, o programa de configuração ou o instalador DLL decreta as contagens de uso. Se qualquer contagem de uso cair para 0, o programa de configuração ou instalador DLL removerá o valor do arquivo e, se o componente for um driver ou um tradutor, excluirá o arquivo. Os arquivos do Driver Manager não devem ser excluídos.  
  
 O formato do valor de contagem de uso do arquivo é mostrado na tabela a seguir.  
  
|Nome|Tipo de dados|Dados|  
|----------|---------------|----------|  
|*caminho completo*|REG_DWORD|*contagem*|  
  
 Por exemplo, suponha que um driver para Informix use os arquivos Infrmx32.dll e Infrmx32.hlp, e suponha que este driver tenha sido instalado duas vezes. Os valores sob a sub-chave SharedDlls para o driver Informix seriam os seguintes:  
  
```  
C:\WINDOWS\SYSTEM32\INFRMX32.DLL : REG_DWORD : 0x2  
C:\WINDOWS\SYSTEM32\INFRMX32.HLP : REG_DWORD : 0x2  
```
