---
title: Os Patches de Software Oracle | Microsoft Docs
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
- ODBC driver for Oracle [ODBC], Oraclesoftware patches
- Oracle software patches [ODBC]
ms.assetid: 1275157b-f4e1-4c24-b273-c02555e261c2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bab4a7bed2fdc63224fd7a2f86757d11375f2cd2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="oracle-software-patches"></a>Patches de Software da Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Patches para os produtos de servidor Oracle e o componente de cliente são necessários para o funcionamento adequado do vários produtos e tecnologias Microsoft, incluindo o Microsoft ODBC Driver for Oracle, o Microsoft OLE DB Provider for Oracle, informações da Internet Services (IIS), serviços de componentes (ou Microsoft Transaction Server, se você estiver usando o Windows NT), e assim por diante.  
  
> [!NOTE]  
>  As instruções a seguir não podem ser completamente precisas porque o site FTP da Oracle está sujeita a alterações.  
  
### <a name="to-download-the-oracle-software-patches"></a>Para baixar os patches de software da Oracle  
  
1.  Conecte-se ao site de FTP público no oracle ftp.oracle.com. A ID de usuário é "anônima" e a senha é seu endereço de email.  
  
2.  Navegue até o seguinte diretório: /server/wgt_tech/server/windowsNT.  
  
3.  Para baixar patches mais relevantes para o Windows 95, Windows 98 e Windows NT/Windows 2000, navegue até a subpasta para sua versão do Oracle — 7.3 ou 8.0. Os dois subdiretórios são /73patchsets e /80patchsets.  
  
4.  Para baixar patches para a tecnologia de rede da Oracle, o SQL * Net ou Net8, navegue até a pasta a seguir: / rede.  
  
 Acessar este site FTP do seu navegador da Web pode não funcionar. Se você tiver problemas, tente usar um cliente FTP "tradicional" ou usar o prompt de comando do DOS.  
  
> [!NOTE]  
>  Como o Oracle correções de bugs nas versões atuais e, em seguida, retrofits-las em versões anteriores, usando os patches de software, é recomendável que você baixe o patch mais recente disponível. Isso é especialmente verdadeiro para os componentes de cliente do servidor Oracle. Se você tiver dúvidas sobre como instalar esses patches, contate o suporte da Oracle.
