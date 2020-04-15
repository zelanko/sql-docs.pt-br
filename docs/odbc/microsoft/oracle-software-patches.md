---
title: Patches de software Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], Oraclesoftware patches
- Oracle software patches [ODBC]
ms.assetid: 1275157b-f4e1-4c24-b273-c02555e261c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1fb577e7b08f6ef332ed35f6d275a5f7ce543ba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292946"
---
# <a name="oracle-software-patches"></a>Patches de software da Oracle
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Patches para os produtos do servidor Oracle e seu componente cliente são necessários para o bom funcionamento de vários produtos e tecnologias da Microsoft, incluindo o Microsoft ODBC Driver for Oracle, o Microsoft OLE DB Provider for Oracle, Internet Information Services (IIS), Component Services (ou Microsoft Transaction Server, se você estiver usando o Windows NT), e assim por diante.  
  
> [!NOTE]  
>  As seguintes instruções podem não ser completamente precisas porque o site Oracle FTP está sujeito a alterações.  
  
### <a name="to-download-the-oracle-software-patches"></a>Para baixar os patches de software Oracle  
  
1.  Conecte-se ao site público da FTP em oracle-ftp.oracle.com. O ID do usuário é "anônimo" e a senha é seu endereço de e-mail.  
  
2.  Navegue até o seguinte diretório: /server/wgt_tech/server/windowsNT.  
  
3.  Para baixar patches mais relevantes para windows 95, Windows 98 e Windows NT/Windows 2000, navegue até o subdiretório para a sua versão do Oracle - 7.3 ou 8.0. Os dois subdiretórios são /73patchsets e /80patchsets.  
  
4.  Para baixar patches para a tecnologia de rede da Oracle, seja SQL*Net ou Net8, navegue até o seguinte diretório: /rede.  
  
 Acessar este site FTP a partir do seu navegador da Web pode não funcionar. Se você tiver problemas, tente usar um cliente FTP "tradicional" ou use o prompt de comando DOS.  
  
> [!NOTE]  
>  Como o Oracle corrige bugs nas versões atuais e, em seguida, os adapta para versões anteriores usando patches de software, é recomendável que você baixe o patch mais recente disponível. Isso é especialmente verdadeiro para os componentes do Oracle Server Client. Se você tiver dúvidas sobre a instalação desses patches, entre em contato com o Suporte Oracle.
