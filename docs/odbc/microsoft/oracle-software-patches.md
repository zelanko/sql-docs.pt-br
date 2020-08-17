---
description: Patches de software da Oracle
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
ms.openlocfilehash: e6bc07ae904b8bb682d9a5cf9eefebe00dc532aa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340682"
---
# <a name="oracle-software-patches"></a>Patches de software da Oracle
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Os patches para os produtos de servidor Oracle e seu componente de cliente são necessários para o funcionamento adequado de vários produtos e tecnologias da Microsoft, incluindo o Microsoft ODBC driver for Oracle, o Provedor Microsoft OLE DB para Oracle, o Serviços de Informações da Internet (IIS), os serviços de componentes (ou o Microsoft Transaction Server, se você estiver usando o Windows NT) e assim por diante.  
  
> [!NOTE]  
>  As instruções a seguir podem não ser completamente precisas porque o site FTP Oracle está sujeito a alterações.  
  
### <a name="to-download-the-oracle-software-patches"></a>Para baixar os patches de software Oracle  
  
1.  Conecte-se ao site FTP público em oracle-ftp.oracle.com. A ID de usuário é "anônima" e a senha é seu endereço de email.  
  
2.  Navegue até o seguinte diretório:/Server/wgt_tech/server/windowsNT.  
  
3.  Para baixar patches mais relevantes para o Windows 95, Windows 98 e Windows NT/Windows 2000, navegue até o subdiretório da sua versão do Oracle-7,3 ou 8,0. Os dois subdiretórios são/73patchsets e/80patchsets.  
  
4.  Para baixar patches para a tecnologia de rede da Oracle, seja SQL * net ou Net8, navegue até o seguinte diretório:/Network.  
  
 O acesso a esse site FTP do navegador da Web pode não funcionar. Se você tiver problemas, tente usar um cliente FTP "tradicional" ou usar o prompt de comando do DOS.  
  
> [!NOTE]  
>  Como o Oracle corrige os bugs nas versões atuais e os recorre a versões anteriores usando patches de software, é recomendável que você baixe o patch mais recente disponível. Isso é especialmente verdadeiro para os componentes do cliente do servidor Oracle. Se você tiver dúvidas sobre como instalar esses patches, entre em contato com o suporte da Oracle.
